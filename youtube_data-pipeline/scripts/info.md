Bronze Bucket Name - youtube-pipeline-bronze-south2
Silver Bucket Name - youtube-pipeline-silver-south2
Gold Bucket Name - youtube-pipeline-gold-south2

Script Bucket-youtube-pipeline-script-south2

SNS ARN - arn:aws:sns:ap-south-2:158527855743:yt-data-alert

glue bronze - yt-data-bronze
 
glue silver - yt-data-silver

glue gold - yt-data-gold


--bronze_database yt-data-bronze
--bronze_table raw_statistics

--silve_bucket youtube-pipeline-silver-south2
--silver_database yt-data-silver
--silver_table clean_statistics
--gold_database yt-data-gold
--gold_bucket  youtube-pipeline-gold-south2
