title: "图片上传"
date: 2015-03-15 10:31:54
tags:
---

图片上传使用 carrierWave Gem，在 Gemfile 中加入 carrierwave '0.10.0'，然后执行：

```
$ bundle install
```

CarrierWave 自带的了一个 generator，用于生成图片上传程序。添加一个图片上传程序，通常有三个步骤：

1. 生成图片上传类：

        $ rails generate uploader PostPicture

2. 在需要图片的 Post 模型中，加入一个属性。这个属性保存图片的地址，字符串形式。

        $ rails generate migration add_picture_to_posts picture:string
        $ bundle exec db:migrate

3. 将 Post 模型与图片上传类 PostPictureUploader 关联起来：

        # app/modals/post.rb
        # ...
        mount_uploader :picture, PostPictureUploader
        # ...
