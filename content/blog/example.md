+++
title = "Example Post"
date = 2022-02-22
insert_anchor_links = true
[extra]
mathjax = true
+++

# Table of Contents

the ToC will grow/shrink with your content, and if it gets too big it'll just overflow into a scroll bar. you can mess with sizes in the css, although it might be a little gross!

## look how long this subsection title is!

see? cool!

# Code Blocks

Code snippets can have filename annotations with the `annotation` shortcode!

{% annotation(language="rust", context="hello-world.rs") %}

```rust, linenos, hl_lines=2 4
fn main() {
    // you can number and highlight lines!
    // won't highlight this one :(
    // using `linenos` and `hl_lines=n`
    println!("hello world!");
}
```
{% end %}

# Blocky Lil Guys

## Asides

 Lorem ipsum dolor sit amet, consectetur adipiscing elit. Phasellus semper, purus sit amet imperdiet dictum, risus diam blandit justo, at dignissim tortor dui sit amet magna. Cras vestibulum maximus nisl ut pharetra. Nullam dignissim auctor euismod. Aenean ut imperdiet diam, sit amet pellentesque ex. Ut sit amet arcu rhoncus, pulvinar mi finibus, aliquam ligula.

{% aside(title="aside") %}
What the fuck did you just fucking say about me, you little bitch? I’ll have you know I graduated top of my class in the Navy Seals, and I’ve been involved in numerous secret raids on Al-Quaeda, and I have over 300 confirmed kills. I am trained in gorilla warfare and I’m the top sniper in the entire US armed forces. You are nothing to me but just another target. I will wipe you the fuck out with precision the likes of which has never been seen before on this Earth, mark my fucking words. You think you can get away with saying that shit to me over the Internet? Think again, fucker. As we speak I am contacting my secret network of spies across the USA and your IP is being traced right now so you better prepare for the storm, maggot. The storm that wipes out the pathetic little thing you call your life. You’re fucking dead, kid. I can be anywhere, anytime, and I can kill you in over seven hundred ways, and that’s just with my bare hands. Not only am I extensively trained in unarmed combat, but I have access to the entire arsenal of the United States Marine Corps and I will use it to its full extent to wipe your miserable ass off the face of the continent, you little shit. If only you could have known what unholy retribution your little “clever” comment was about to bring down upon you, maybe you would have held your fucking tongue. But you couldn’t, you didn’t, and now you’re paying the price, you goddamn idiot. I will shit fury all over you and you will drown in it. You’re fucking dead, kiddo.
{% end %}

## Callouts

callouts are cool too!

{% callout(type="info") %}
asides are scrollable :)
{% end %}

{% callout(type="note") %}
callouts will expand as much as they can without conflicting with asides!

callouts have other cool features, like...
- inline markdown!!!! this was the coolest 4 me
- that's it lol
{% end %}

Donec accumsan nulla at enim maximus, ac hendrerit elit bibendum. Aenean vitae felis lorem. Nunc in tristique sem, nec semper lorem. Cras ultrices eget justo id ullamcorper. Vestibulum ante ipsum primis in faucibus orci luctus et ultrices posuere cubilia curae;



# Definitions

definitions are highlighted like this! it uses a regular old definition list under the hood for that sweet sweet semantic goodness

{% definition(term="distributed system") %}
a system that's distributed!
{% end %}

that's about it for this one but i'm adding some text here to pad things out



# Math

math is enabled under the `[extra]` options in the front matter

{% annotation(context="the front matter of this doc!") %}

```toml
+++
title = "Example Post"
date = 2022-02-22
insert_anchor_links = true
[extra]
mathjax = true
+++
```

{% end %}

## inline

inline \\(a^3 + b^3 = c^3\\) sick sick sick

## block

\\[
    \int_{-\infty}^\infty
    \hat f(\xi)\,e^{2 \pi i \xi x}
    \,d\xi
\\]

## aligned
\\[
    \\begin{align}
        a + b &= c\\\\
        a^2 + b^2 &= c^2
    \\end{align}
\\]

# Third

Vivamus viverra augue dui, ac feugiat ligula venenatis vitae. Aliquam in risus consequat, iaculis urna nec, vehicula nisi. Aliquam vulputate varius luctus. Fusce eu nunc nec dui aliquam mattis. Fusce sit amet pellentesque tellus, et auctor elit. Duis eget risus at massa pulvinar feugiat.