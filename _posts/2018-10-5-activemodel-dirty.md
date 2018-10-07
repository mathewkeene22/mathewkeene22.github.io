---
layout: post
title:  "ActiveModel::Dirty"
subtitle: "A quick and dirty run down"
tags: [Ruby on Rails, Programming]
categories: [tech]
---

## Cleaning Up With ActiveModel Dirty
ActiveModel::Dirty is a handy library that allows you to detect when an object has changed from the model level. I've found this to be incredibly helpful when you only want to run a method after a specific change occurs. You are able to track these changes by appending `_changed?` to the attribute being listened to.

Often times I will use ActiveModel:Dirty in a call back like so:

```ruby
after_save :is_hungry

def is_hungry
  if is_hungry_changed?
    self.order_pizza
  end
end
```

These dirty methods also give us the ability to view what changes have been made. This can be done by appending the attribute we are expecting to change with `_change`, resulting in an array that contains the previous and new values.

```ruby
matty.favorite_pizza = 'bbq chicken'
matty.favorete_pizza_changed? # => true
matty.favorite_pizza_change # => ['mushroom and olive', 'bbq chicken']
```

Another powerful option Dirty provides is the ability to return true or false when a change meets a specific requirement

```ruby
matt.preferred_crust # => 'New York'
matty.preferred_crust = 'Sicilian'
matty.preferred_crust_changed?(from: 'New York', to: 'Sicilian') # => true
```

There are a handful of other useful methods you can read about [in the Rails documentation](https://api.rubyonrails.org/classes/ActiveModel/Dirty.html) for a deeper look into this library.
## 🍕 🍕 🍕 🍕 🍕 🍕 🍕 🍕 🍕 🍕 🍕 🍕 🍕 🍕 🍕 🍕 🍕 🍕
