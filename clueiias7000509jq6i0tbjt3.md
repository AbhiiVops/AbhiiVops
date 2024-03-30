---
title: "Running Headless Chrome with Puppeteer on AWS Lambda"
datePublished: Sun Jan 14 2024 18:30:00 GMT+0000 (Coordinated Universal Time)
cuid: clueiias7000509jq6i0tbjt3
slug: running-headless-chrome-with-puppeteer-on-aws-lambda
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1711827580056/9a2b2500-284d-44d7-9369-315fa9fa44fb.png
tags: cloud, aws, web-development, cloud-computing, aws-lambda, puppeteer

---

Today we will learn how to run **Chrome headless** in **AWS lambda** via **Puppeteer** in a **serverless environment** using **Lambda layers**.

Every owner of a laptop or phone knows what a web browser is and uses it every day. Even this article was written and read in a web browser. However, not everybody knows that browsers can be run in a headless mode and be used for resolving various tasks besides simple surfing on the internet.

In this article you will learn what headless browsers are, what are the use cases and how to implement AWS serverless services and run Chrome headless in AWS Lambda.

## What are Headless Browsers?

The general definition of a headless browser is pretty easy — it is a browser without a user interface. Such a browser persists all the normal functionality, but since there is no need to render any content to the real screen, such a browser consumes less memory, doesn’t require GPU, is more performant and can be controlled programmatically.

These features in allow developers to effectively utilize browser possibilities for implementing web crawlers, running UI tests, taking screenshots, tracking web page’s performance, automating web site interactions and other things. Further in the article, we will focus on headless Chrome from AWS Lambda and explore how to implement and utilize both.

## How to Try Running a Headless Chrome?

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1711819716922/df04ab18-32b5-4a0f-a99f-d95c071f7e31.png align="center")

Before learning how to run Headless Chrome on AWS Lambda, let’s go deeper into the functionalities of Headless Chrome. If you have Google Chrome installed on your computer, you can try to run it in a headless mode right now. For example, it is possible to convert any web page into a PDF file with a single command. Open the command line, navigate to a folder you’d like to save the PDF file to and execute the following command:

```bash
$ chrome --headless --disable-gpu --print-to-pdf https://imagini.co
```

The chrome browser will start without any user interface, it will silently load Imagini’s website, render it in the memory instead of the real screen and create the output.pdf file on the disk in a few seconds.

If it doesn’t happen and you see an error in the console saying that such a command is not found, you need to tell your system that command “chrome” stands for executing Chrome browser which is located in its installation folder. If you are a Windows user, you may try following the [path setting instructions](https://www.computerhope.com/issues/ch000549.htm) in order to resolve this issue.

If you are using Mac, this can be easily done with the next command:

```bash
alias chrome="/Applications/Google\ Chrome.app/Contents/MacOS/Google\ Chrome"
```

Now, try to rerun the initial command. If for some reason it still doesn’t work, don’t worry, as after reading the below sections you will be able to run a much more cool example on AWS!

## Complex Scenarios with Headless Chrome

Having the ability to create a PDF or an image of a web site with a single command is cool, but what about more complex scenarios? Is it possible to give some instructions the browser should perform on the page? Definitely yes!

## Chrome DevTools Protocol

Chrome DevTools Protocol or [CDP](https://chromedevtools.github.io/devtools-protocol/) is a special way of communicating with the running browser instance by sending special commands via a network connection to the particular port opened by that instance. CDP allows debugging and fully controlling the browser programmatically, meaning that it is possible to write a script that will perform various tasks in the browser. For example, you may develop an application that will run a browser, navigate to a particular page, click buttons, fill in forms, dump contents, take pictures and many other things. Of course, it is possible to write such applications from scratch, including managing the network connection, messaging and strictly following the protocol on your own. However, the usage of special libraries will save your time and prevent mistakes in the implementation.

## Puppeteer

One of the great libraries exposing a great high level API for communicating with Chrome or Chromium is [Puppeteer](https://pptr.dev/). It was originally written in [Node.js](https://www.techmagic.co/web-development/nodejs) and then also ported to Python and .Net, but there are some [alternatives](https://github.com/ChromeDevTools/awesome-chrome-devtools#automation) for other programming languages. Puppeteer allows you to write elegant and readable code and concentrate on the desired functionality and scenarios rather than proper network communication. It is also a serverless web scraper for Chrome headless that provides automation. In the practice part of this article, you will explore running headless Chrome via Puppeteer and coding an app with Nodej.js

## Test Project: Screenshot Service

The best way of understanding things is by trying them yourself. The idea of a test project is in implementing a web based app able to respond with a picture of how a particular website looks on a particular screen size. The application expects 2 parameters to be sent as a part of the user's request: URL of the website to be captured and the screen resolution. For example, request to:

```bash
https://example.com/capture?url=https://Imagini.co&screen=1280,800
```

will result in a screenshot of how the Imagini website looks in 1280 x 800 screen resolution. Hosting such apps using a **serverless** approach on the AWS Lambda would be the ideal option from both performance and cost perspectives.

## Why AWS Lambda?

![](https://www.techmagic.co/blog/content/images/2022/10/Inner-02.-Chrome-with-AWS-Lambda--Why-AWS-Lambda-@2x.png align="left")

[AWS Lambda](https://aws.amazon.com/lambda/) is a **serverless computing service** provided by Amazon Web Services, it is incredibly cost-effective and scalable. The main concept of **AWS Lambda functions** is running code in response to various events like HTTP requests, changes in file storage, messages from other AWS services, emails and other things happening in the application.

In turn, you are billed only for the time taken to execute your function and you never pay for the idle. Code runs in the virtual stateless containers where one container is processing only one event at a time and if there are 20 simultaneous incoming events AWS will immediately create 20 containers to handle the spike and will close those down after load decreases. Service is fully managed by Amazon and developers don’t need to worry about infrastructure and may concentrate on the code and application logic instead. The benefits and limitations of AWS Lambda are not the topics of this article, but the few above facts already make AWS Lambda an ideal option for our test project!

## Implementing a Service

Before diving into the code, you will need to have Node.js [installed](https://nodejs.org/en/download) on your machine. You will also need to install Serverless Framework — a superior command line tool for deploying and managing applications based on AWS Lambda. Finally, you should have an AWS account and you should [configure](https://www.serverless.com/framework/docs/providers/aws/guide/credentials/) Serverless Framework with your AWS credentials — it will be not possible to deploy applications without doing this. The whole preparation process may take a while, but the final result will definitely be worth it.

## Create Project and Install Dependencies

Open terminal, navigate to a directory where you’d like to keep project files and run the following command:

```bash
$ serverless create --template aws-nodejs --path screenshot-service
```

It will create a folder “screenshot-service” with some initials files inside. Then, navigate into this folder and run commands for initializing node.js project and installing puppeteer.

```bash
$ npm init
```

Simply confirm all the prompts and then run the package:

```bash
$ npm install puppeteer-core
```

Note that you actually install the “puppeteer-core” module instead of “puppeteer”. The reason for that is because you do not need a browser itself which is included in a “puppeteer” module, instead you want to have only the communication functionality. You may probably ask “How then the browser will get into Lambda?” — it is a good question and you will find the answer in the below section.

### Serverless Configuration

Open the ***serverless.yml*** file, which is the main configuration file for your application and may consist of dozens of [properties](https://www.serverless.com/framework/docs/providers/aws/guide/serverless.yml/) describing future service and the resources required. Here are all the settings required for the test project, so you can simply replace the content of your ***serverless.yml*** file these:

```yaml
service: screenshot-service
frameworkVersion: '2'

provider:
  name: aws
  runtime: nodejs12.x
  region: eu-west-1

functions:
  capture:
    handler: handler.capture # refers to function capture in handler.js
    events:
      — http: # trigger function via http request
          path: capture
          method: get
    memorySize: 1536 # RAM size for the function
    timeout: 15
    layers: # reference to the already existing layer with Chrome
      — arn:aws:lambda:eu-west-1:764866452798:layer:chrome-aws-lambda:20
```

Most of the properties are quite self-descriptive, but the last line is worth paying a bit more attention to because it is actually the answer to the question about how the browser gets into the Lambda environment. That is done via AWS Lambda Layers — a feature for extending Lambda environments with any necessary content such as libraries, custom runtimes, binaries (like headless Chrome) and other dependencies. It is possible either to create and publish own layers or use publicly available layers prepared by third-party organizations, open-source enthusiasts and communities. Preparing a layer with a custom binary or binary itself might be a tricky process as it requires execution files to be firstly compiled in an environment similar to the AWS Lambda system. So for simplicity in this test project, we will refer to the [existing](https://github.com/shelfio/chrome-aws-lambda-layer#available-regions) and deployed layer by pasting its arn (unique resource identifier in AWS) into the “layers” property in ***serverless.yml*** file. However, it worth noting that in a real project you also may use third-party layers, but you should deploy them to your AWS account in order to prevent potential failures if the author removes the published layer.

## Coding the Function

Now it is time to add some javascript code responsible for processing requests. Open the ***handler.js*** file and replace its content with a following:

```javascript
const puppeteer = require("puppeteer-core");
const chrome = require("chrome-aws-lambda");

const capture = async  (event) => {
  const { queryStringParameters } = event;
  if (!queryStringParameters || !queryStringParameters.url || !queryStringParameters.screen) {
    return { statusCode: 403 };
  }

  const { url } = queryStringParameters;
  const [width, height] = queryStringParameters.screen.split(",");

  if (!width || !height) {
    return { statusCode: 403 };
  }

  const browser = await puppeteer.launch({
    executablePath: await chrome.executablePath,
    args: chrome.args
  });

  const page = await browser.newPage();
  await page.setViewport({
    width: Number(width),
    height: Number(height)
  });

  await page.goto(url);
  const screenshot = await page.screenshot({ encoding: "base64" });

  return {
    statusCode: 200,
    body: <img src="data:image/png;base64,${screenshot}">,
    headers: { "Content-Type" : "text/html" }
  };
}

module.exports = { capture };
```

The code above is quite self-descriptive and understandable, so even if you are not a JavaScript expert, you should see the main flow of instructions: check that URL and screen size were defined correctly, then open browser, open new page, set the desired viewport size, navigate to the destination, capture screenshot and send it.

### Deployment

This is probably the easiest part. The only thing you need to do is running the following command:

```bash
$ serverless deploy
```

If AWS credentials are configured correctly, the deployment process starts and may take a minute or two. In the end you will see the result, including an URL of your service ready to use!

## Testing the Final Solution

Copy the URL of your function endpoint, paste it into your browser’s address bar, but don’t submit for now as you first need to add the proper query parameters at the end of the URL, for example:

```bash
?url=https://Imagini.co&screen=800,600
```

Hit “Enter” and wait for a few seconds and see the result image!

You may change the desired URL and screen size and re-run the query, but remember to use a valid URL with a valid protocol like ***“http://” or “https://”*** prepended.

## What’s Next?

![](https://www.techmagic.co/blog/content/images/2022/10/Inner-03.-Chrome-with-AWS-Lambda--What-s-Next-@2x.png align="left")

The possibility of running headless Chrome on AWS Lambda reveals a wide spectrum of various useful solutions to build and benefit from them for developers, testers and end users. In this article, you learned the core principles of executing headless browsers in serverless environments, but in order to effectively develop a real-world app you need to continue investigating CDP and learning libraries like Puppeteer. You will also need to have a grasp of **serverless concepts, AWS Lambda quotas and the Lambda layers management** to be able to improve your application or resolve emerging issues. Keep in mind that practicing is the best way to consolidate your knowledge.

***If you've found this exploration of running Chrome headless on AWS Lambda intriguing, show your appreciation with a 💗. Don't let this be the end of your journey into the realm of serverless wonders and cloud technologies. Stay connected for more insightful content by subscribing to our newsletter and following us for future awe-inspiring blogs.***

***Get ready to embark on a continued adventure filled with tech wonders and captivating insights. Stay tuned for more exciting discoveries in the world of serverless computing and beyond.***