# Elastic Beanstalk Fundamentals

Created: May 9, 2019 7:17 PM
Updated: May 9, 2019 8:39 PM

A developer centric view of developing on AWS.

It uses pretty much every service used in the high-level 3-tier web app, though controls it in a single view/service.

**Pricing**

Free, you only pay for underlying instances/services.

**Managed**

- Instance configuration / OS is handled by beanstalk.
- Deployment strategy is customizable though handled by Beanstalk.

**Architecture Models:**

****1) Single Instance Deployment: good for dev

2) LB + ASG: great for production on pre-production web applications

3) ASG only: great for non-web apps in prod (workers…)

**Components**

- Application
- Application Version: each deployment is assigned a version
- Environment name (dev, test, prod)

Apps can be deployed to ENV 1 and then promoted through the pipeline.

Allows for rollbacks to X version.

**Support**

- Go
- Java SE
- ….ALL OF THEM

**Deployment**

- All at once: fastest deployment though instances aren’t available to serve traffic for a while (downtime)
    - Best for quick iterations in dev environment
    - No additional costs
- Rolling: update few instances at a time before moving forward to the next bucket
    - Application starts running below
        
        capacity (can set bucket size)
        
    - Instances are stoped in batches (all-in-one in sections)
    - No additional cost
    - Can take LONG TIME (many instance and small bucket size)
- Rolling with additional batches: Like rolling, though spins up new instances to move the batch to so there is never any downtime
    - Apposite of rolling (not under capacity)
    - Small additional cost
    - Can take long time as well
    - Adds new servers and does health checks BEFORE removing old servers
- Immutable: Creates whole new ASG of Instances and swaps out with the current ASG when marked healthy
    - Zero downtime
    - New code deployed to new instances on a temporary ASG
    - Highest cost, at double capacity
    - Deployment takes the longest
    - VERY quick rollback (just terminate temp ASG)
    - Great and safe PROD choice
- Blue / Green:
    - Not a real feature, but zero downtime release facility. Creates a new “stage” environment to deploy new version too, which can be validated independently and rolled back in case of issues. Using Beanstalk, “swap urls” when done with the environment test.
    - Route53 can be weighted to send minimal traffic to stage.

**TIP**

When uploading/deploying a zip file manually from Mac, you may run into a hidden files error. The fix is to run the following command AGAINST the zip file being uploaded:

$ zip -d filename.zip __MACOSX/\*