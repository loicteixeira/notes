# Self-Serving Analytics in the Cloud (with Tableau)

Explaining how we are lazy fucks and need graphs instead raw data, but also that there are good and bad ways of showing things. Use [pre-attentive visual attributes](https://learnforeverlearn.com/preattentive/) to communicate efficiently.

People who know the data should ask the questions. The first question might be crap but can be refined with iteration.

Tableau is in the AWS Marketplace and can connect to different databases sources (RDS, S3, Redshift, Athena).

Netflix case study: Events logged with Kafka and saved into S3 (which goes througth various state of cleaning) then pushed to Redshift. Tableau sit on top of Redshift.

Data amount is reduced (or aggregated) as you go warmer: Cold (S3) > Warm (Redshift) > Tableau (Hot)