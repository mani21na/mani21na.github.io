---
layout: post
title:      "CRUD with "accepts_nested_attributes_fo"
date:       2020-02-17 17:42:55 -0500
permalink:  crud_with_accepts_nested_attributes_for
---


I decided to use nested attributes to store items in Lists table instead of items columns.  And I had to go through a lot of trial and error. I want to keep a record of it.

As  first step, I added the line `**accepts_nested_attributes_for: items**` to the List model. And we modified the list_params method of ListsController like this

```
  def list_params
    params.require(:list).permit(
		    :user_id, 
		    :subject, 
				**items_attributes: [:item_no, :item, :quantity, :done]**
				)
  end 
```

I also set the validates of the items table to the itme model.

```
    validates :item, presence: true, if: :done_checked?
    validates :quantity, presence: true, if: :item_is_exist?

    def item_is_exist?
        !(item == "") 
    end

    def done_checked?
        done
    end
```

With the above settings, the new and create methods worked fine.

```
  def new
    @list = List.new
    @num = 0
    10.times do
      @num += 1
      @list.items.build(item_no: "#{@num}")
    end
  end

  def create
    @list = List.new(list_params)
    if @list.valid?
      @list.save
      redirect_to user_path(current_user.id)
    else
      render :new
    end
  end
```

However, the update method showed unexpected movement. This is the first my struggle. Failed to update the data, adding new items to the list. The reason was that Rails didn't find the data to update because I didn't make the: id of the item a Strong parameter. So I fixed the problems like this

```
  def list_params
    params.require(:list).permit(
		    :user_id, 
		    :subject, 
				items_attributes: [:item_no, :item, :quantity, :done, **:id**]
				)
  end 
```

The next problem was that when deleting a list, the items in the list were left in the database without being erased.

```
  def destroy
    @list.items.destroy
    @list.destroy
    redirect_to user_path(current_user.id)
  end
```

I found out that another configuration is required to use this delete feature.

> the accepts_nested_attributes_for has some neat features for deleting associations. If we pass the allow_destroy: true argument to accepts_nested_attributes_for, it will destroy any members from the attributes.
> 

So I did fix it again in ListController and List model.

```
  def list_params
    params.require(:list).permit(
		    :user_id, 
		    :subject, 
				items_attributes: [:item_no, :item, :quantity, :done, :id, ** '_destroy'**]
				)
  end 
	
	
	accepts_nested_attributes_for :items, **:allow_destroy => true**
```

But this setup alone was not perfect.
The reason is that I set the item's validates to the item model. So I set the following setting to solve this problem.

```
validates_associated :items
```


