# [Enkoder][h-e] for [Nanoc][].

A minor, but useful, modification of [Dan Benjamin's][db] [Hivelogic Enkoder Rails plugin][h-e-r], by [Christopher Boone][hpm].

The Enkoder library provides a [Nanoc][] helper that can be used to protect email addresses (or other information) by obfuscating them using JavaScript code. The only way to decrypt the JavaScript is to actually run it, hiding the results from email-harvesting robots while revealing them to real people.

Note: There's no guarantee here -- the only way to be completely safe is to not publish your address at all.


## More information:

For more examples and to see the full functionality of the Enkoder, have a look at:

* Enkoder's permanent page on the web: [http://hivelogic.com/enkoder][h-e]
* The Rails Enkoder plugin on Github: [http://github.com/dan/hivelogic-enkoder-rails][h-e-r]
* The Nanoc project site: [http://nanoc.stoneship.org/][Nanoc]
* Nanoc's Mercurial project: [http://projects.stoneship.org/hg/nanoc/][n-hg]
* Nanoc's Github mirror: [http://github.com/ddfreyne/nanoc][n-gh]
* The Nanoc user manual: [http://nanoc.stoneship.org/docs/][n-docs]
* The helpers section, in the Nanoc user manual: [http://nanoc.stoneship.org/docs/4-basic-concepts/#helpers][n-docs-h]
* The Nanoc Trac (wiki and issue tracker): [http://projects.stoneship.org/trac/nanoc][n-t]
* Nanoc's API documentation: [http://nanoc.stoneship.org/docs/api/3.1/][n-api]

Also, you might be interested in [Arno Hautala's][] [ObfuscateEmail filter][], which takes a slightly different approach.


## Installation:

Just drop [the `helpers.rb` file][h-rb] and [the `helpers` folder][h-f] into the `/lib` directory in your project.

Or, if you already have a `helpers.rb` file and a `helpers` folder in your project's `/lib` directory, then add [the `enkoder.rb` file][e-rb] to your `/lib/helpers` directory, and add the following to your `helpers.rb` file:

    require 'lib/helpers/enkoder'
    include Nanoc3::Helpers::Enkoder


## Usage:

There are two methods:

`enkode( html )`

This method accepts a block of html (or any text) and returns an enkoded JavaScript.

The second method is:

`enkode_mail( email, link_text, title_text=nil, subject=nil )`

This method takes an email address, the text to show to the viewer, optional title text (what's seen when somebody hovers over the link), and optional subject for the email, and returns an enkoded email address link.


## Examples:

To enkode a single email address, one could just do:

`<%= enkode_mail('user@domain.com','click here') %>`

And the following link would be returned (enkoded as JavaScript):

`<a href="mailto:"user@domain.com" title="">click here</a>`

Adding a title and subject text would require the second two optional fields:

`<%= enkode_mail('user@domain.com','click here', 'email me', 'enkoder') %>`

And we'd get back (enkoded as JavaScript):

`<a href="mailto:"user@domain.com?subject=enkoder" title="email me">click here</a>`

Of course we can also enkode many email addresses on the fly:

`<% @users.each do |user| %> <p><%= enkode_mail(@user.email,@user.name) %></p> <% end %>`

To enkode a snippet of XHTML, we can do:

`<%= enkode("<p>This block will be hidden from spambots.</p>") %>`

We could protect a link or block of XHTML from being indexed like this:

`<%= enkode('Try and find <a href="secret.html">this</a>, google!') %>`

We could have anything we wanted in that block, XHTML, links, email addresses, etc.


## License:

Copyright (c) 2009 Hivelogic Corporation.

This plugin is released under the GPL license. See [the LICENSE file][license] for details.


[h-e]: http://hivelogic.com/enkoder
[db]: http://hivelogic.com/
[h-e-r]: http://github.com/dan/hivelogic-enkoder-rails
[hpm]: http://hypsometry.com/
[h-rb]: http://github.com/cboone/nanoc-enkoder/blob/master/helpers.rb
[license]: http://github.com/cboone/nanoc-enkoder/blob/master/LICENSE
[Nanoc]: http://nanoc.stoneship.org/
[n-gh]: http://github.com/ddfreyne/nanoc
[n-docs-h]: http://nanoc.stoneship.org/docs/4-basic-concepts/#helpers
[n-docs]: http://nanoc.stoneship.org/docs/
[n-hg]: http://projects.stoneship.org/hg/nanoc/
[n-t]: http://projects.stoneship.org/trac/nanoc
[n-api]: http://nanoc.stoneship.org/docs/api/3.1/
[h-f]: http://github.com/cboone/nanoc-enkoder/tree/master/helpers/
[Arno Hautala's]: https://github.com/fracai
[ObfuscateEmail filter]: https://gist.github.com/830730
