![CLEVER DATA GIT REPO](https://raw.githubusercontent.com/mikesdatawork/images/master/git_mikes_data_work_banner_01.png "Mikes Data Work")

# Use Distribution Groups For SQL Database Mail
** Post Date: June 29, 2015 **





## Contents    
- [About Process](##About-Process)  
- [SQL Logic](#SQL-Logic)  
- [Build Info](#Build-Info)  
- [Author](#Author)  
- [License](#License)       

## About-Process

<p>You'll find many examples online on how to configure SQL Database Mail. These work great to demonstrate the process, but some might get confused on what to actually use for the 'recipients'. It's better to simply use a distribution group. If you need to add more people to the email notifications simply add them to the distribution group. Otherwise; you would end up hardcoding email addresses in and out of your notification steps within your jobs. Not a good idea, and completely inefficient. Have more than one 'type' of alerts going on? Create more distribution groups and apply them accordingly. Do not mettle around directly in your notification logic if you can help it.
Sample notification logic:</p>   

   
## Logic
```SQL
declare @server_name varchar(255)
declare @job_name varchar(255)
declare @message_subject varchar(255)
declare @message_body varchar(max)
 
set @server_name = (select @@servername )
set @job_name = (select name from msdb.dbo.sysjobs where @jobid = convert(uniqueidentifier, $(escape_none(jobid))))
set @message_subject = (select 'Job Failure on Server: ' + @server_name + ' Job: ' + @job_name
set @message_body = @message_subject + char(10) + char(10) + 'The Job failed at step (step name):'
 
EXEC msdb.dbo.sp_send_dbmail
@profile_name = 'SQLDatabaseMailProfile'
, &lt;em&gt;@recipients = 'AnotherEmailAddress@mydomain.com', 'AnotherEmailAddress', 'AnotherEmailAddress'&lt;/em&gt; &lt;img src="https://mikesdatawork.files.wordpress.com/2015/06/image002.png" alt="" width="14" height="14" class="alignnone size-full wp-image-568" /&gt; NOT efficient.
, @recipients = 'sqladminalerts@mydomain.com' &lt;img src="https://mikesdatawork.files.wordpress.com/2015/06/image002.png" alt="" width="14" height="14" class="alignnone size-full wp-image-568" /&gt; More efficient. Use distribution groups.
, @subject = @message_subject
, @body = @message_body
```

![Distribution Groups]( https://mikesdatawork.files.wordpress.com/2015/06/image0032.jpg "SQL Database mail")
 


[![WorksEveryTime](https://forthebadge.com/images/badges/60-percent-of-the-time-works-every-time.svg)](https://shitday.de/)

## Build-Info

| Build Quality | Build History |
|--|--|
|<table><tr><td>[![Build-Status](https://ci.appveyor.com/api/projects/status/pjxh5g91jpbh7t84?svg?style=flat-square)](#)</td></tr><tr><td>[![Coverage](https://coveralls.io/repos/github/tygerbytes/ResourceFitness/badge.svg?style=flat-square)](#)</td></tr><tr><td>[![Nuget](https://img.shields.io/nuget/v/TW.Resfit.Core.svg?style=flat-square)](#)</td></tr></table>|<table><tr><td>[![Build history](https://buildstats.info/appveyor/chart/tygerbytes/resourcefitness)](#)</td></tr></table>|

## Author

- ** Github Gist**
- ** Twitter**
- ** Wordpress** "MikesDataWork"

[![Gist](https://img.shields.io/badge/Gist-MikesDataWork-<COLOR>.svg)](https://gist.github.com/mikesdatawork)
[![Twitter](https://img.shields.io/badge/Twitter-MikesDataWork-<COLOR>.svg)](https://twitter.com/mikesdatawork)
[![Wordpress](https://img.shields.io/badge/Wordpress-MikesDataWork-<COLOR>.svg)](https://mikesdatawork.wordpress.com/)

   
## License
[![LicenseCCSA](https://img.shields.io/badge/License-CreativeCommonsSA-<COLOR>.svg)](https://creativecommons.org/share-your-work/licensing-types-examples/)

![Mikes Data Work](https://raw.githubusercontent.com/mikesdatawork/images/master/git_mikes_data_work_banner_02.png "Mikes Data Work")

