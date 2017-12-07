

# Simple Metrics Tutorial Part 1: Metrics Collection
The IBM Cloud Data Services Developer Advocacy team built this lightweight web-tracking app to record user actions on our site’s AJAX-enabled search engine page. [Follow the tutorial](http://developer.piwik.org/guides/tracking-javascript-guide)
and learn how we use the open source Piwik® web analytics app to collect information and Node.js® to store that data in Cloudant. Then try it yourself by implementing tracking on a demo app we provide. Here in Part 1, we focus on data collection. When you’re done, you can try Part 2, where we show how to visualize the data you’ve gathered.


##How it works

Here’s an architectural overview of our metrics collector. Its middleware component lives on [IBM Bluemix](https://www.bluemix.net/) (IBM’s open cloud platform for building, running, and managing applications) and serves `tracker.js` and `piwik.js`, which perform the metrics collection work and persist metrics data to the database. We use Cloudant as our database, a NoSQL JSON document store based on Apache CouchDB™. 

<img src="http://developer.ibm.com/clouddataservices/wp-content/uploads/sites/47/2015/07/collector-arch-1024x327.png">

## Deploy to IBM Cloud

###One-Click Deployment

The fastest way to deploy this application to IBM Cloud is to click this **Deploy to IBM Cloud** button. Or, if you prefer working from the command line, skip to the **Deploy Manually** section.

[![Deploy to IBM Cloud](https://metrics-tracker.mybluemix.net/stats/d3f1fccf9886fdc7656070f84cabd8dc/button.svg)](https://bluemix.net/deploy?repository=https://github.com/ibm-watson-data-lab/metrics-collector)

**Don't have an IBM Cloud account?** If you haven't already, you'll be prompted to sign up for a Bluemix account when you click the button.  Sign up, verify your email address, then return here and click the the **Deploy to IBM Cloud** button again. Your new credentials let you deploy to the platform and also to code online with Bluemix and Git. If you have questions about working in IBM Cloud, find answers in the [IBM Cloud Docs](https://www.ng.bluemix.net/docs/).

###Deploy Manually

#### Configure Cloud Foundry

If you haven't already, [install the Cloud Foundry command line interface and connect to Bluemix](https://www.ng.bluemix.net/docs/#starters/install_cli.html).


#### Create Backing Services

Create a Cloudant service within IBM Cloud if one has not already been created:

    $ cf create-service cloudantNoSQLDB Lite metrics-collector-cloudant-service

#### Deploy

To deploy to IBM Cloud, simply:

    $ cf push

> **Note:** You may notice that IBM Cloud assigns a URL to your application containing a random word. This is defined in the `manifest.yml` file where the `random-route` key set to the value of `true`. This ensures that multiple people deploying this application to IBM Cloud do not run into naming collisions. To specify your own route, remove the `random-route` line from the `manifest.yml` file and add a `host` key with the unique value you would like to use for the host name.

**Privacy Notice:**

Refer to https://github.com/IBM/metrics-collector-client-node#privacy-notice

To disable deployment tracking, remove the following line from `server.js`:

```
require("metrics-tracker-client").track();
```

Once that line is removed, you may also uninstall the `metrics-tracker-client` npm package.

## Try the Tutorial

Once you deploy, [follow the tutorial](https://developer.ibm.com/clouddataservices/simple-metrics-tutorial-part-1-metrics-collection/) to understand exactly how this app works and to learn how to collect user behavior data for your own web app or page. 

When you're done, move on to [Part 2](https://developer.ibm.com/clouddataservices/simple-metrics-tutorial-part-2-d3-and-json/) of this tutorial, where you’ll learn how to display collected data graphically in a report.


_<sup>© "Apache", "CouchDB", "Apache CouchDB" and the CouchDB logo are trademarks or registered trademarks of The Apache Software Foundation. All other brands and trademarks are the property of their respective owners.</sup>_

