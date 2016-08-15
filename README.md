# Jekyll Disqus Comments Importer

## Migrate Disqus comments into static YAML files for use with [Staticman][staticman].

`disqus_comments.rake` assumes that the Disqus blog has **not been deactivated**. If it is unreachable via the Disqus API, this plugin will not be able to fetch comments.

This plugin will download post comments from Disqus and cache them in `_data/comments/<post-slug>/` folders at the root of the Jekyll site.

### Installation

Copy the following files to your Jekyll site folder.

* `_rake/disqus_comments.rake`
* `Rakefile` (Not necessary if you already have a Rakefile that loads `_rake/*`)

### Obtain Disqus API Public Key

To use the plugin, you will need to obtain a `public key` from the [Disqus API](http://disqus.com/api/applications/) and add it to your `_config.yml`.

1. [Register new application](https://disqus.com/api/applications/register/)
2. Setup application. Suggested configuration below:

```
Label: <Name of application> eg. Jekyll Disqus importer
Description: Convert comments into static files.
Website:
Domains: disqus.com
Default Access: Read only
```

Add the following lines to your `_config.yml`

```
comments:
  disqus:
    short_name: YOUR-DISQUS-FORUM-SHORTNAME-HERE
    api_key:    YOUR-DISQUS-PUBLIC-KEY-HERE
```

### Importing Disqus Comments

Import comments from Disqus by running `rake disquscomments`

### Troubleshooting

When running `rake disquscomments` you may see warnings like:

```
Comments feed not found: <domain.com>/post-slug/
```

This likely means no comments exist for a given post. It could also mean `ident` is wrong and needs to be modified to match the Disqus identifier of each post.

To verify Disqus identifiers:

1. [Export Disqus comments](https://disqus.com/admin/discussions/export/) as XML.
2. Download and open XML file.
3. Look for `<link>` elements. This is what Disqus is using to identify each comment feed. eg. `<link>https://mademistakes.com/mastering-paper/contour-drawing/</link>`

By default the plugin attempts to get comments using the default Disqus identifier of `domain.com/post-id/`. It assumes `url` has been set in `_config.yml`. If you used something else you will need to modify the following line in `disqus_comments.rake`:

```
# site.url + post.id + trailing slash
ident    = site['url'] + post.id + '/'
```

## License

Copyright &copy; 2013 Patrick Hawks and licensed under dual licensed under [The MIT License](http://opensource.org/licenses/MIT) and the [GNU General Public License, version 2 or later](http://opensource.org/licenses/gpl-2.0.php), except for the files noted below.

You don't have to do anything special to choose one license or the other and you don't have to notify anyone which license you are using.

***

`./Rakefile` from [jekyll-bootstrap](http://jekyllbootstrap.com/) and licensed under [The MIT License](http://opensource.org/licenses/MIT)

Copyright &copy; 2012 Jade Dominguez

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the 'Software'), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED 'AS IS', WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.

[staticman]: https://staticman.net/