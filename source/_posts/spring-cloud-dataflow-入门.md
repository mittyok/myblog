---
title: spring cloud dataflow 入门
date: 2016-12-02 10:35:15
tags:
  - spring cloud
  - dataflow
  - task
  - batch
  - job
---

## 最初为什么选择Spring
- make j2ee easier
- loose-coupling through interfaces, dependency injection, aspect-oriented programming
- sought to make the entire java ecosystem easier
- security, various types of database, data integration, and now cloud-native microservices
- spring is headed now with regard to reactive programming.

## H2
```
The development of H2 was started in May 2004, but it was first published on December 14th 2005. The main author of H2, Thomas Mueller, is also the original developer of Hypersonic SQL. In 2001, he joined PointBase Inc. where he wrote PointBase Micro, a commercial Java SQL database. At that point, he had to discontinue Hypersonic SQL. The HSQLDB Group was formed to continued to work on the Hypersonic SQL codebase. The name H2 stands for Hypersonic 2, however H2 does not share code with Hypersonic SQL or HSQLDB. H2 is built from scratch.
```

## Spring Cloud Task
```
Spring Cloud Task allows a user to develop and run short lived microservices using Spring Cloud and run them locally, in the cloud, even on Spring Cloud Data Flow. Just add @EnableTask and run your app as a Spring Boot app (single application context).
```

## Task Demo
```
@SpringBootApplication
@EnableTask
public class SampleTask {

    @Bean
    CommandLineRunner commandLineRunner() {
        return new HelloWorldCommandLineRunner();
    }

    public static void main(String[] args) {
        SpringApplication.run(SampleTask.class, args);
    }

    private class HelloWorldCommandLineRunner implements CommandLineRunner {

        @Override
        public void run(String... strings) throws Exception {
            System.out.println("Hello World!");
        }
    }
}
```

## Spring Batch
在一些特定的情况下，我们会有这样的需求，我们需要批量的执行一些业务操作。这些业务操作一般都有这样的特点：

1. 涉及到的数据量较大
2. 不需要人工干预
3. 处理较为复杂
4. 需要自动的处理

典型的操作如：日结或者月结的一些计算，通知等类似的场景。。。

### 典型的场景
1. 周期性的批量处理
2. 并行作业
3. 基于消息驱动的业务处理
4. 失败后支持手动或者定时重启的场景
5. 一些步骤需要按顺序执行的
6. 作业需要支持事务的情况


## Concept
1 Job = Many Steps
1 Step = 1 REAT-PROCESS-WRITE or 1 Tasklet

Job = {Step 1 -> Step 2 -> Step 3}

## Example
Example code.
### Main Class
```lang=java
@EnableTask
@EnableBatchProcessing
@SpringBootApplication
public class BatchJobApplication {
 
    public static void main(String[] args) {
        SpringApplication.run(BatchJobApplication.class, args);
    }
}
```
### Job Configuration
```lang=java
@Configuration
public class JobConfiguration {
 
    private static Log logger
      = LogFactory.getLog(JobConfiguration.class);
 
    @Autowired
    public JobBuilderFactory jobBuilderFactory;
 
    @Autowired
    public StepBuilderFactory stepBuilderFactory;
 
    @Bean
    public Job job() {
        return jobBuilderFactory.get("job")
          .start(stepBuilderFactory.get("jobStep1")
          .tasklet(new Tasklet() {
             
              @Override
              public RepeatStatus execute(StepContribution contribution, 
                ChunkContext chunkContext) throws Exception {
                 
                logger.info("Job was run");
                return RepeatStatus.FINISHED;
              }
        }).build()).build();
    }
}
```

### Chunk-Oriented Processing
```
Chunk oriented processing refers to reading the data one at a time, and creating 'chunks' that will be written out, within a transaction boundary.
```

## Spring Cloud Dataflow

### Tap