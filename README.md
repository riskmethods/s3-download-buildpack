# S3 Download Buildpack

This is a [Heroku Buildpack](https://devcenter.heroku.com/articles/buildpacks)
that can download files from private [Amazon S3](http://aws.amazon.com/s3/)
buckets. It gives you a way of deploying pre-built code to
[Heroku](http://www.heroku.com/) without making it publicly accessible.

## Usage

    $ heroku config:add BUILDPACK_URL=https://github.com/paleozogt/s3-download-buildpack.git

    $ cat .buildpack-s3-downloads
    AWS_ACCESS_KEY_ID=AKIA0000000000000000
    AWS_SECRET_ACCESS_KEY=xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx
    s3://bucket/path/to/tarball.tgz /output_path/filename.tgz
    s3://bucket/path/to/somethingelse.zip /output_path/some_other_file.zip

You probably want to use an [IAM key](http://aws.amazon.com/iam/) with limited
access. This code only requires `s3:GetObject` access to files.

If you don't want to check your IAM keys into revision control, you can store
them in Heroku's config system. Keys specified in the .buildpack-s3-downloads
file have precedence over keys in the config system.

    $ heroku config:add BUILDPACK_URL=https://github.com/paleozogt/s3-download-buildpack.git
    $ heroku config:add AWS_ACCESS_KEY_ID=AKIA0000000000000000
    $ heroku config:add AWS_SECRET_ACCESS_KEY=xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx

    $ cat .buildpack-s3-downloads
    s3://bucket/path/to/tarball.tgz /output_path/filename.tgz

## Licence

MIT license, see LICENSE.txt for details.
