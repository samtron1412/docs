[TOC]

# Introduction
>`Ruby on Rails`, often simply referred to as `Rails`, is an *open source web application framework* which runs via the *Ruby* programming language. It is a [full-stack](http://en.wikipedia.org/wiki/Solution_stack) framework: it allows creating pages and applications that *gather* information from the web server, talk to or *query* the database, and *render* templates out of the box. As a result, Rails features a routing system that is independent of the web server.

## [Install](http://rubyonrails.org/download/)
`gem install rails`

## Technical

### MVC
A *model* in the Ruby on Rails framework maps to a table in a database, and a Ruby file. Use [Active Record pattern](http://www.martinfowler.com/eaaCatalog/activeRecord.html). [Guide](http://guides.rubyonrails.org/active_record_basics.html)

A *controller* is a component of Rails that responds to external requests from the web server to the application by determining which view file to render. Rails encourages developers to use RESTful routes, which include actions such as: create, new, edit, update, destroy, show, and index. [Guide](http://guides.rubyonrails.org/action_controller_overview.html)

A *view* in the default configuration of Rails is an erb file, which is compiled to HTML at run-time. [Guide](http://guides.rubyonrails.org/layouts_and_rendering.html)

### Tools
[Scaffolding](http://en.wikipedia.org/wiki/Scaffold_(programming))

[WEBrick](http://en.wikipedia.org/wiki/WEBrick), a simple Ruby web server.

[Rake](http://en.wikipedia.org/wiki/Rake_(software)), a build system.

Ruby on Rails is separated into various packages, namely *ActiveRecord* (an object-relational mapping system for database access), *ActiveResource* (provides web services), *ActionPack*, *ActiveSupport* and *ActionMailer*.

## Philosophy and design
>Ruby on Rails emphasizes the use of well-known [software engineering patterns](http://en.wikipedia.org/wiki/Software_design_pattern) and principles, such as [active record pattern](http://en.wikipedia.org/wiki/Active_record_pattern), [convention over configuration](http://en.wikipedia.org/wiki/Convention_over_configuration) (CoC), [don't repeat yourself](http://en.wikipedia.org/wiki/Don%27t_repeat_yourself) (DRY), and [model–view–controller](http://en.wikipedia.org/wiki/Model%E2%80%93view%E2%80%93controller) (MVC).

`"Convention over Configuration"` means a developer only needs to specify unconventional aspects of the application. For example, if there is a class Sale in the model, the corresponding table in the database is called sales by default. It is only if one deviates from this convention, such as calling the table "products sold", that the developer needs to write code regarding these names. Generally, Ruby on Rails conventions lead to less code and less repetition.

`"Don't repeat yourself"` means that information is located in a single, unambiguous place. For example, using the ActiveRecord module of Rails, the developer does not need to specify database column names in class definitions. Instead, Ruby on Rails can retrieve this information from the database based on the class name.

# User guide
`rails new <your_app>`

## Model
### Basic Active Record

    `rails g model <model name at singular> [<columns and type>]`

    >E.g. `rails g model Article title:string text:text`

### Migration
- Create
`rails g migration `

- Run
`rake db:migrate [RAILS_ENV=development/production/test/...]`

- Rollback (lastest migration or number step migration)
`rake db:rollback [STEP=3/4/...]`

- Redo: rollback and do migrate again
`rake db:migrate:redo`

### Validation

### Callback

### Association

### Query interface

## View
### Layout and rendering

### Form helper

## Controller
### Basic Action Controller

    `rails g controller <controller name at plural> [<actions in controller>]`

    >E.g. `rails g controller Welcome index`

### Rails Routing
- Show routes
    `rake routes`

## Testing
- Unit test: RSpec, Test::Unit, Cucumber
- Simulation user's interaction: Capybara, Factory Girl

## Deploy
### [Terminal multiplexer](https://en.wikipedia.org/wiki/Terminal_multiplexer)
A terminal multiplexer is a software application that can be used to multiplex several virtual consoles, allowing a user to access multiple separate terminal sessions inside a single terminal window or remote terminal session. It is useful for dealing with multiple programs from a command line interface, and for separating programs from the Unix shell that started the program.

>Running process after terminate ssh session

1. Use `&` after command run process background. Example: `rails s &`
2. Running `rails s` after terminate ssh connection by [screen](https://www.gnu.org/software/screen/) package.
`screen` will create new shell to run `rails s`, detach with `Ctrl + A + D` and go back to screen with `screen -r`. [Wikipedia](https://en.wikipedia.org/wiki/GNU_Screen)

3. Use [tmux](http://tmux.sourceforge.net/) same `screen`. [Wikipedia](https://en.wikipedia.org/wiki/Tmux)

### Find process use port
`sudo lsof -i tcp:80`

`sudo netstat -nlp|grep 80`

### Run server

- Commands
    + Default run at port 3000:
    `rails s`

    + When port less than 1024 (0-1023) process need root privileged:
    `rvmsudo rails s -p 80`

    + Port great than 1024:
    `rails s -p <port>`

- Errors
    + EADRRINUSE: port conflict
    + EACCESS: port conflict

# [Tutorial - Michael Hartl, Learn Rails by example](http://www.railstutorial.org/)




