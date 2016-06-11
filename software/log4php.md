[TOC]

# Overview
[log4php](https://logging.apache.org/log4php/)

# Basic usage

	// Load log4php, if use autoload by composer then can eliminate it.
	include('log4php/Logger.php');

	// Tell log4php to use our configuration file.
	Logger::configure('config.xml');

	// Fetch a logger
	$log = Logger::getLogger('myLogger');

	// Start logging
	$log->trace("My first message.");   // Not logged because TRACE < WARN
	$log->debug("My second message.");  // Not logged because DEBUG < WARN
	$log->info("My third message.");    // Not logged because INFO < WARN
	$log->warn("My fourth message.");   // Logged because WARN >= WARN
	$log->error("My fifth message.");   // Logged because ERROR >= WARN
	$log->fatal("My sixth message.");   // Logged because FATAL >= WARN

# log4.xml

	<?xml version="1.0" encoding="UTF-8"?>
	<configuration xmlns="http://logging.apache.org/log4php/">
	    <appender name="default" class="LoggerAppenderRollingFile">
	        <param name="file" value="/var/log/map_tool/file.log" />
	        <param name="maxFileSize" value="1MB" />
	        <param name="maxBackupIndex" value="2" />
	        <param name="append" value="true" />
	        <layout class="LoggerLayoutPattern">
	            <param name="conversionPattern" value="%date{Y-m-d H:i:s.u} %-5level  %file(%line) %msg%n" />
	        </layout>
	    </appender>
	    <appender name="db" class="LoggerAppenderRollingFile">
	        <param name="file" value="/var/log/map_tool/db.log" />
	        <param name="maxFileSize" value="1MB" />
	        <param name="maxBackupIndex" value="2" />
	        <param name="append" value="true" />
	        <param name="threshold" value="debug" /><!-- out put level: debug, not out putlevel : info -->
	        <layout class="LoggerLayoutPattern">
	            <param name="conversionPattern" value="%date{Y-m-d H:i:s.u} %-5level  %file(%line) %msg%n" />
	        </layout>
	    </appender>
	    <appender name="console" class="LoggerAppenderEcho">
	        <layout class="LoggerLayoutPattern">
	            <param name="conversionPattern" value="%date{Y-m-d H:i:s.u} %-5level  %file(%line) %msg%n" />
	        </layout>
	    </appender>
	    <appender name="mail" class="LoggerAppenderMailEvent">
	        <layout class="LoggerLayoutPattern">
	            <param name="conversionPattern" value="%date{Y-m-d H:i:s.u} %-5level  %file(%line) %msg%n" />
	        </layout>
	        <param name="to" value="tran.son@rivercrane.vn" />
	        <param name="from" value="logger@example.com" />
	        <param name="subject" value="map_toolBatch" />
	        <param name="smtpHost" value="192.168.33.15" />
	        <param name="port" value="25" />
	    </appender>
	    <root>
	        <level value="info" />
	        <appender_ref ref="default" />
	        <!--<appender_ref ref="console" />-->
	        <!--<appender_ref ref="mail" />-->
	    </root>
	    <logger name="db">
	        <level value="debug" />
	        <appender_ref ref="db" />
	    </logger>
	</configuration>
