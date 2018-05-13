# springcloudsluethzipkin



1)	Add below dependencies
	<dependency>
		<groupId>io.zipkin.java</groupId>
		<artifactId>zipkin-server</artifactId>
	</dependency>
	<dependency>
		<groupId>io.zipkin.java</groupId>
		<artifactId>zipkin-autoconfigure-ui</artifactId>
		<scope>runtime</scope>
	</dependency>


Enable below annotation

import zipkin.server.EnableZipkinServer;


@SpringBootApplication
@EnableZipkinServer


Bootstrap Zipkin application


2)	Write Client for zipkin sleuth
<dependency>
			<groupId>org.springframework.cloud</groupId>
			<artifactId>spring-cloud-starter-sleuth</artifactId>
		</dependency>
	<dependency>
			<groupId>org.springframework.cloud</groupId>
			<artifactId>spring-cloud-sleuth-zipkin</artifactId>
		</dependency>


Add below Bean configuration


import org.springframework.cloud.sleuth.sampler.AlwaysSampler;

	@Bean
	public AlwaysSampler defaultSampler() {
	  return new AlwaysSampler();
	}


Add below configuration in bootstrap.yml file

spring:  
  application:
    name: customer-service
  logging:
    pattern:
      console: "%clr(%d{yyyy-MM-dd HH:mm:ss}){faint} %clr(${LOG_LEVEL_PATTERN:-%5p}) %clr([${springAppName:-},%X{X-B3-TraceId:-},%X{X-B3-SpanId:-},%X{X-Span-Export:-}]){yellow} %clr(${PID:- }){magenta} %clr(---){faint} %clr([%15.15t]){faint} %clr(%-40.40logger{39}){cyan} %clr(:){faint} %m%n${LOG_EXCEPTION_CONVERSION_WORD:-%wEx}"
    level:
      org.springframework: WARN
      org.hibernate: WARN    





