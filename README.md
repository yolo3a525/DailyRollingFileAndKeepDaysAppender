# DailyRollingFileAndKeepDaysAppender
对log4j DailyRollingFileAppender的改进，通过参数配置，可以只保留多少天的文件。

对log4j-1.2.17.jar这个版本的改造，其他版本拿去只要编译可以通过应该就没问题

1.log4j的配置

	log4j.appender.AA=org.apache.log4j.DailyRollingFileAndKeepDaysAppender
	log4j.appender.AA.File=d:/log/o2o.log
	#存放日志的格式
	log4j.appender.AA.DatePattern='.'yyyyMMdd
	log4j.appender.AA.layout=org.apache.log4j.PatternLayout
	log4j.appender.AA.layout.ConversionPattern=%d{HH:mm:ss} %p [%c] - %m%n
	#下面就是配置最多存放日志的天数
	log4j.appender.AA.keepDays=2

2.把类放到你自己的工程下就可以了

仅仅增加了如下代码

	/*delete  before keepdays file*/
	if(keepDays != 0){
		String deleteFileName =  fileName+sdf.format(new Date(now.getTime() - keepDays * 24 * 60 * 60 * 1000));
		File target  = new File(deleteFileName);
		    if (target.exists()) {
		      target.delete();
		      LogLog.debug("delete log file -> "+ deleteFileName);
		    }
	}
