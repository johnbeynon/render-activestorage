# render-activestorage

A demo of using [Rails ActiveStorage](https://edgeguides.rubyonrails.org/active_storage_overview.html) with Render.

## Deployment on Render

[![Deploy to Render](https://render.com/images/deploy-to-render-button.svg)](https://render.com/deploy)

## About

This uses [Render Disks](https://render.com/docs/disks) as the storage mechanism for ActiveStorage.

In `storage.yml` it defines a disk service named `render` with the root set to the mount point of the disks (as defined in `render.yaml` or via the dashboard).

```
render:
  service: Disk
  root: '/opt/activestorage-data'
```

and then in `production.rb` ActiveStorage is configured to use this service:

```
  # Store uploaded files on the local file system (see config/storage.yml for options).
  config.active_storage.service = :render
```

## Notes

It's definitely worth being aware of the present [limitation of Disks](https://render.com/docs/disks#application-considerations). Noteably:

* Disks can only be attached to a single instance - ie. you can scale up your app/service. For Rails, given this limitation then using a service like Amazon S3 may suit better.