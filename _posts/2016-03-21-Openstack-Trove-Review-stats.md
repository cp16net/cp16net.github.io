---
layout: post
title: "Openstack Trove Review Stats"
categories:
    - dev
tags:
    - "openstack"
    - "trove"
slug: "openstack-trove-review-stats"
markup: "rst"
---

# Overview

It has been helpful to look at the review stats for the OpenStack Project Trove
over time to see the involvement of the community. During the Trove weekly team
meeting we have used the reviewstats tool to get data points and track them in
a spreadsheet so that we can graph the commits, patches, and reviews to see
where we stand.

## How-To

Clone the reviewstats repo from the openstack-infra project on github.

{% highlight bash %}
git clone https://github.com/openstack-infra/reviewstats.git
{% endhighlight %}

I've created a venv just for this project and installed the project into it.

Then I created a simple helper bash script that includes the credentials needed
for the scripts. Pull your username and password for gerrit from [gerrit
settings](https://review.openstack.org/#/settings/http-password)

{% highlight bash %}
reviewers -p projects/trove.json -r10 -d 7 -u ${GERRIT_USERNAME} -P ${GERRIT_PASSWORD}
openreviews -p projects/trove.json -u ${GERRIT_USERNAME}
{% endhighlight %}


After that setup, we can run this script and get the data for the last week on
the project.

We've added this data to a [google spreadsheet](http://bit.ly/1VQyg00) and graphed it over the last
year.
