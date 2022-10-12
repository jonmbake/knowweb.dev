---
layout: default
title: Cross site scripting (XSS)
parent: Mitigations
grand_parent: Security
---

**Web dev concern level:** 3/10 -- Less of a concern since most frameworks handle HTML escaping by default.

Often times, web applications display user entered data on to the page. For example, a visitor to a blog makes a comment on a post:

<pre>
Cool post, man!
I learned a lot!
</pre>

When the blog post page gets rendered, the following HTML is outputted:

```
<p>Cool post, man!</p>
<p>I learned a lot!</p>
```

What happens if the blog commenter makes a comment that contains valid HTML? For example:

<pre>
Cool post, man!
&lt;script&gt;alert('this website has been hacked!')&lt;&#47;script&gt;
I learned a lot!
</pre>

If the blog is vulnerable to an XSS attack, the comment HTML will be rendered like:


```
<p>Cool post, man!</p>
<p><script>alert('this website has been hacked!')</script></p>
<p>I learned a lot!</p>
```

Notice the `script` tag is not HTML-escape so the page will interpret the contents of the tag as JavaScript. Now every visitor to the blog post will have an alert telling them that "this website has been hacked!" 😲

![picture 1](/images/you-have-been-hacked-alert.png)  

## Mitigation

To protect against XSS, any user entered values must be HTML-escaped. For the above example, the correct HTML output for the `script` portion of the blog comment would is:

```
&lt;script&gt;alert('this website has been hacked!')&lt;&#47;script&gt;
```

The JavaScript will no longer be evaluated. All is safe (at least from a XSS-perspective).

Fortunately, all modern web frameworks escape HTML by default. For example, if in react you have a component like:

```
class BlogComment extends React.Component {
  render() {
    return <p>{this.props.userEnteredComment}</p>;
  }
}
```

`this.props.userEnteredComment` will be HTML-escaped by default. Side note: React does offer a way to render unescaped HTML via [#dangerouslysetinnerhtml](https://reactjs.org/docs/dom-elements.html#dangerouslysetinnerhtml).