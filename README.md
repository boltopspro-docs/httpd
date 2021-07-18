<!-- note marker start -->
**NOTE**: This repo contains only the documentation for the private BoltsOps Pro repo code.
Original file: https://github.com/boltopspro/httpd/blob/master/README.md
The docs are publish so they are available for interested customers.
For access to the source code, you must be a paying BoltOps Pro subscriber.
If are interested, you can contact us at contact@boltops.com or https://www.boltops.com

<!-- note marker end -->

# Configset: httpd

![CodeBuild](https://codebuild.us-west-2.amazonaws.com/badges?uuid=eyJlbmNyeXB0ZWREYXRhIjoiQzBrZDErRHRhT1o1YmVFM2ROMlVIT3NFQm1iUkpZSTd1cWNVUEltc2h1ajAydnpoc2lmVVpVNEIrdmQxZ3VIbkYyTDd6SjVhUmpmZXRuV3BFY01EcmdBPSIsIml2UGFyYW1ldGVyU3BlYyI6IkMycjJyanNZYmZaeUJvNXEiLCJtYXRlcmlhbFNldFNlcmlhbCI6MX0%3D&branch=master)

[![BoltOps Badge](https://img.boltops.com/boltops/badges/boltops-badge.png)](https://www.boltops.com)

This lono configset will install, configure and run the httpd or apache2 webserver.

## What are lono configsets?

Lono configsets allow CloudFormation [cfn-init](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/cfn-init.html) [configsets](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-resource-init.html) that are typically embedded in the template to be reusable.  More info: [Lono Configsets docs](https://lono.cloud/docs/configsets/).

## Usage

Add the configset to Gemfile:

```ruby
gem "httpd", git: "https://github.com/boltopspro-docs/httpd"
```

Use `configset` to enable it for a [lono blueprint](https://lono.cloud/docs/core/blueprints/).  Here's a example with a blueprint named demo:

configs/demo/configsets/base.rb:

```ruby
configset("httpd", resource: "Instance")
```

This adds the configset to the `resource` with the logical id `Instance` in your CloudFormation template.  The configset is added to the [Resources[].Metadata.AWS::CloudFormation::Init](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-resource-init.html) attribute of the `Instance` resource.

Here's an another example adding to a `LaunchConfig` resource:

```ruby
configset("httpd", resource: "LaunchConfig")
```

And another example adding to a `LaunchTemplate` resource:

```ruby
configset("httpd", resource: "LaunchTemplate")
```

## Set the html content

You can set the html content of the created `/var/www/html/index.html` file with configset variables. Example:

configs/demo/configsets/httpd/variables.rb:

```ruby
@html =<<~EOL
<h1>My test page</h1>
<p>My test content. Set with configs/demo/configsets/httpd/variables.rb.</p>
EOL
```

Learn more here: [Configset Variables Docs](https://lono.cloud/docs/configsets/variables/)
