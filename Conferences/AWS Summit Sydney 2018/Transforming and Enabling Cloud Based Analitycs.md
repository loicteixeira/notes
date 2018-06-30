# Transforming and Enabling Cloud Based Analytics

## Legacy

Old dashboard is written multi languages and isn't maintainable

Getting result is a tedious manual process (download locally, upload to specific software, run analytics, results).

## SIRCA (Analytics) Gateway

Streamlined process. Data is already there, jump straight to running analytics.

You can import your own data an join on existing data if needed.

Onboarding with notebooks, training videos, webinars, data definitions and FAQs.

### Delivering value at multiple levels

1. Leverage power of new data collections
2. Compute in the cloud to boost analytics
3. Lightning speed
4. Enabling you to explore and analyse
5. Allowing you to visualise
6. Collaborate with peers
7. Cost savings in software, hardware and bandwidth

### Architecture

Mostly run in `talend` but sometimes run some `Python`, then process with `Hive`.

Interfaced to user with `databricks`.

### Challenges and Lessons Learnt

- Ingesting data as early as possible
  - issue: didn't do enough analysis of the data to make it easy to consume
- Work closely with your data analysis
- Development and production of Databricks environments should have the same featuers enabled
  - issue: multi-tenancy with Databricks
- Consider how you will manage changes to dataset schemas
- Pre-purchase reserved instances
  - issue: higher cost than expected
- Spark does not guarantee the order of ingested data
  - issue: parallel ingestion don't output the expected order

### Features important to the users

- Share analysis
- Schedule jobs
- Teaching aid in classrooms
- Visualise results
- Collaborate with nominated colleagues
- Publish dashboards
- Choice or programming language to execute analytics
  - Third-party packages can be imported in notebooks