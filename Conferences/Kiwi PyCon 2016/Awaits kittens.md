---
url: https://youtu.be/RMdb9FWO4S4
---

# await kittens()

Lots of kittens 🙀

Libraries:
- `asyncio` from `Python 3.4` to define and run your own asynchronous functions.
- `aiohttp` to query (replaces `requests`) and serve (replaces `flask`) asynchronously.

Async primer:

`async def`
- Creates an async function.
- Allows the use of the async and await keywords.
- Prevents the use of yield and yield from

`await x`
- 'pauses' the function until x is resolved.
- Internally uses yield from added in Python 3.3

First async:
```python
import asyncio
import aiohttp

async def my_first_kitten(image_url):
    async with aiohttp.get(image_url) as img:
        img.raise_for_status()
        content = await img.read()

    # IO cannot be done asynchronously
    with open('first_async_kitten.jpg', 'wb') as file:
        file.write(content)

async def async_main():
    await my_first_kitten('https://c1.staticflickr.com/7/6201/6128762944_72a4e5d2af_o_d.jpg')

if __name__ == '__main__':
    loop = asyncio.get_event_loop()
    loop.run_until_complete(async_main())
```

Running in parallel:
```python
async def async_main():
    (_, _) = await asyncio.gather(
        get_kitten(1, 'https://c2.staticflickr.com/6/5601/15497374938_7239eb4d9f_k.jpg'),
        get_kitten(2, 'https://c2.staticflickr.com/4/3288/4006914394_bcd2fe6539_o.jpg')
    )
```

Rate limitting:
```python
MAX_REQUESTS = 2
TIME_FRAME = .5

api_blocking_queue = []
api_lock = asyncio.BoundedSemaphore(MAX_REQUESTS)

async def locked_my_call(url):
    # Prepare the call so we can wait on it in multiple places
    async with api_lock:
        while len(api_blocking_queue) >= MAX\_REQUESTS:
        done, _ = await asyncio.wait(api_blocking_queue, return_when=asyncio.FIRST_COMPLETED)

    for item in done:
        # Remove the done items so the length reduces.
        api_blocking_queue.remove(item)

    # We have space in the queue to add a new delay.
    # This will cause the next API call to wait for at most `TIME_FRAME` before running.
    api_blocking_queue.append(asyncio.ensure_future(asyncio.sleep(TIME_FRAME)))

    return await my_call(url)
```

See [full script](https://github.com/leesdolphin/await-kittens/blob/c39bd20d64c797fdfcb0b44aa52073d728e17d9f/code/kittens/now_what/rate_limiting.py).