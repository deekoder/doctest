
# Doctor : An Open Source Documentation Server


Doctor is a documentation server which serves MD (markdown)  files from github. Using Doctor we can easily decouple 
document serving and document content in a clean manner. At Minio, we have several github repositories for our server, 
client utility and SDKs. We also have full examples and recipes to help our developers onboard to our products. A simple UX which could categorize and display our content is what we needed. 

![Doctor](https://github.com/deekoder/doctest/blob/master/Doctor_Site.png?raw=true "Doctor Category Dashboard")

Doctor is a rails app with a very simple architecture. The two main models in this project are Documents and Categories. 

## Category - Document Relationship 
Category and Documents have what we refer to as has_many/belongs_to relationship.

## Category Model

Category can be thought of as a logical folder that holds a collection of documents.

```ruby
 class Category < ActiveRecord::Base
  has_many :documents , dependent: :destroy
end
```

## Document Model

Documents on the other hand are simply links that have a name and belong to a particular Category

```ruby
class Document < ActiveRecord::Base
  belongs_to :category
end
``` 


Now let's look at what columns make up Category and Model. Category has a title and a description fields. Document has name, description
link and reference variable to category_id. This honors the has_many/belongs_to relationship between these two models. Why we 
decided to use links alone is because we really liked decoupling documents from the document server. We had pretty good documentation
in github so we really wanted to maintain a single copy of md files that needed to be aggregated and presented to our users. 
 
### Category UX 
![Category]( https://github.com/deekoder/doctest/blob/master/Category_2.png?raw=true "Doctor Category Dashboard")

### Document UX
![Documents]( https://github.com/deekoder/doctest/blob/master/Documents_2.png?raw=true "Doctor Documents Dashboard")
 
## Platformization
To make it a real platform, we need to add an admin user persona that is able to easily create categories and documents 
objects to set up the docs site. Hence we have User Model also. Right now in this release there is only the notion of an
Administrator User, but the User model leaves room for possibilities to create types of Users such as Editors, Reviewer
and Approvers for a later time. Doctor is booted with a seed file which creates a default admin user. Users of Doctor can
edit the db/seeds.rb file to change the admin user credentials.

### Admin Dashboard
![Admin]( https://github.com/deekoder/doctest/blob/master/DashBoard_2.png?raw=true "Admin Dashboard")

Collaboration was another key requirement for us. We take a non trivial stand when it comes to having our community contribute 
to our project. So we provide the "Suggest Edits" feature where any developer that uses our docs can suggest changes by clicking
on Suggest Edits and sending us a simple PR with their changes. This was a feature we could not find in hosted solutions, 
CMS solutions and frameworks. 

## Customization
There are 2 levels of customization possible in Doctor. One can edit Brand details from within the dashboard and change project 
name, links in the header and footer. See screenshot below :

### Brand Customizations
![Brand](https://github.com/deekoder/doctest/blob/master/brand.png?raw=true "Brand Dashboard")

The second level of customization can be done on variables.scss file. You may change fonts, colors, backgrounds, text colors, borders
sidebar to your needs. In the next version of Doctor some of these tuning will also be available through the dashboard.

```css
$body-bg: #fafafa;

/*--------------------
  Font
--------------------*/
$font-family: 'Lato', sans-serif;
$font-family-glyph: fontAwesome;
$font-family-headings: 'Lato', sans-serif;
$font-family-mono: 'Roboto Mono', monospace;
$font-size: 17px;
$line-height: 1.5;
$line-height-heading: 1.1;


/*--------------------
  Text Colors
--------------------*/
$heading-color: #5c6267;
$link-color: #4FA2E4;
$text-color: #7c8287;
$text-muted: #9a9a9a;
$text-strong: #4e4e4e;


$headings-font-weight: 400;


/*--------------------
  Border Colors
--------------------*/
$line-color: #efefef;
$input-border: #f4f4f4;


/*--------------------
  Sidebar
--------------------*/
$sidebar-bg: #f1f1f1;


/*--------------------
  Colors
--------------------*/
$blue: #2196F3;
$light-blue: #03A9F4;
$red: #F44336;
$cyan: #00BCD4;
$teal: #009688;
$green: #4CAF50;
$light-green: #8BC34A;
$orange: #FF9800;
$amber: #FFC107;
$grey: #9E9E9E;
$blue-gray: #607D8B;
$dark: #252b2f;

```
 
## Why did we build Doctor 
We really wanted a simple way to render our documentation from github. We loved markdown since it was easy for our non developers
to create/edit documentation. We didn't want to waste our precious resources to maintain multiple copies of documentation. We
needed to involve the community in making our documentation better. And finally we needed a nice looking site which would 
champion our content, brand and licenses without any web gimmicks. After evaluating frameworks, CMS solutions and cloud hosted 
platforms, we built our own simple platform. 

Doctor enhancements and issue list can be found at https://github.com/minio/doctor/issues


 




