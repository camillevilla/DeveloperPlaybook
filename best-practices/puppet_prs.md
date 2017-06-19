# Puppet PRs

Occasionally, a developer may need a system level configuration change made to a machine. Perhaps the most common example is when a dev needs ssh access to a machine to be able to kick off a capistrano task. In this case, we encourage devs to make a pull request to the Puppet repository where such configuration is mannaged.

To issue a PR to the DLSS puppet repository, first make sure you have a local clone of the repo. Inside, check out a branch off of `production` on which to do your work. By convention the name of the branch should include your sunetid, so that operations knows who is issuing the PR:

```
git checkout -b sunetidFeature
git branch --set-upstream-to=origin/production  
```

The configuration to set up ssh access for a user on a server typically lives in the `hieradata/node` directory, where the file name is the fqdn of the server, followed by the `eyaml` extension. For example,

```
requests-dev.stanford.edu.eyaml
```

if you needed access to the requests development machine.  Within that file, you will find a hiera key for `k5users`, whose value is an array of sunetids. You will need to add your own sunetid to that hash like so:

```
role::params::app_user:
  requests:
    k5users:
      - mysunetid
      - yoursunetid
```

Next, add, commit, and push the change in your branch to github for review, making sure to set your local feature branch to track a remote feature branch:

```
git add .
git commit -m 'your commit message'
git push origin sunetidFeature
```

 Once the PR has been reviewed and merged into the production branch, the puppetmaster will apply the configuration on its next run, usually within an hour, or a friendly operations team member will apply the change to the server by running the puppet agent manually.
