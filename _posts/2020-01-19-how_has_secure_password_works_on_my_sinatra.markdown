---
layout: post
title:      "How has_secure_password works on my Sinatra"
date:       2020-01-20 04:45:51 +0000
permalink:  how_has_secure_password_works_on_my_sinatra
---



Adds methods to set and authenticate against a BCrypt password. This mechanism requires you to have a XXX_digest attribute. Where XXX is the attribute name of your desired password.

The following validations are added automatically:

1. Password must be present on creation
2. Password length should be less than or equal to 72 bytes
3. Confirmation of password (using a XXX_confirmation attribute)


For using this magic, you need to add bcrypt-ruby (~> 3.1.2) to Gemfile.
```
gem 'bcrypt-ruby', '~> 3.1.2'
```

Then setting a XXX_digest in Migrate.
```
class CreateUsers < ActiveRecord::Migration[5.2]
  def change
    create_table :users do |t|
      t.string :password_digest
    end 
  end
end
```

And add one line in your model
```
class User < ActiveRecord::Base
  has_secure_password
end

```




