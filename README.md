bosh-cloudfoundry-poc
=====================

To get a general idea of cloudfoundry try to read at least this document before starting:

+ https://github.com/StarkAndWayne/bosh-cloudfoundry/blob/master/docs/concept.md

If you want to go a bit further watch the following material:

+ http://www.youtube.com/watch?feature=player_embedded&v=dRR9NLiEmR0
+ http://vimeo.com/42248020 

For noobs questions:
+ for bosh(and bosh-bootstap too!) go here:
+ for cloudfoundry(and bosh-cloudfoundry too!) go here:

Steps to get cloud foundry running on aws with bosh.

before starting clean security groups , private keys and instances that bosh could have create in previous tries.

use bosh gem directly from github, the current release breaks!
so that means:

```
  
  git clone git://github.com/StarkAndWayne/bosh-bootstrap.git
  cd bosh-boostrap
  gem build bosh-bootstrap.gemspec 
  gem install pkg/bosh-bootstrap-0.6.0.gem 
```
on your local:
```
bosh-bootstrap deploy
```
IMPORTANT: DURING THE INSTALATION LEAVE THE DEFAULT AWS REGION AND DONT LEAVE THE PASSWORD IN BLANK!

if you get the following error durring the instalation:

uploading stemcell (00:12:02)                                                 
Creating VM from...          |ooo                | 2/11 00:12:17  ETA: 00:55:10/usr/local/lib/ruby/gems/1.9.1/gems/aws-sdk-1.6.9/lib/aws/core/client.rb:318:in `return_or_raise': Invalid availability zone: [us-east-1b] (AWS::EC2::Errors::InvalidParameterValue)
  from /usr/local/lib/ruby/gems/1.9.1/gems/aws-sdk-1.6.9/lib/aws/core/client.rb:419:in `client_request'

Do this:
edit the .bosh_bootstrap/manifest.yml and add the availability zone to the bosh_resources_cloud_properties:
```
...snip...
 28 bosh_resources_cloud_properties:
 29   instance_type: m1.medium
 30   availability_zone: us-east-1a # <--- THIS ONE , RIGHT HERE!
 ...snip...
```
run the command again and if it is still failing try with a diferent availability_zone till it works.

--------------
by now you should have a bosh machine working.
you should be able to follow this tutorial to intall cloudfoundry with bosh:
https://github.com/StarkAndWayne/bosh-cloudfoundry
