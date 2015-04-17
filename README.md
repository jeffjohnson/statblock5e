A Web Component statblock for D&D 5E
====================================

Statblock5e provides an easy way to display a creature statblock that looks
almost exactly like the statblocks from the 5th edition D&D Monster Manual.

<div align="center">
  <img src="http://i.imgur.com/K2fcFz0.png" />
</div>

This is implemented as a set of custom elements following the [Web
Components][web-components] specs: [HTML Imports][html-import], [Custom
Elements][custom-elements], [Shadow DOM][shadow-dom] and the HTML5 [template][]
element.

Since Chrome is [currently the only browser][wc-status] that implements all of
the above specs, **statblock5e only works in Chrome.** (Firefox is close to
providing all the necessary support but it's all behind flags.)

<div align="center">
  <p><a href="http://jeffjohnson.github.io/statblock5e/demo.html">
     <b>LIVE DEMO</b></a>
  </p>
</div>

**There are _no_ dependencies** (JavaScript or otherwise), **this is entirely
self-contained**.

There's very little JavaScript actually; just a bit of boilerplate that
registers the elements and some minor logic for computing the ability modifiers
for the ability table. Other than that, it's pure HTML, CSS & SVG.

Here's the markup that produced the above picture. **No user-level CSS or
JavaScript is necessary.**

```html
<stat-block>
  <creature-heading>
    <h1>Animated Armor</h1>
    <h2>Medium construct, unaligned</h2>
  </creature-heading>

  <top-stats>
    <property-line>
      <h4>Armor Class</h4>
      <p>18 (natural armor)</p>
    </property-line>
    <property-line>
      <h4>Hit Points</h4>
      <p>33 (6d8 + 6)</p>
    </property-line>
    <property-line>
      <h4>Speed</h4>
      <p>25ft</p>
    </property-line>

    <abilities-block data-str="14"
                     data-dex="11"
                     data-con="13"
                     data-int="1"
                     data-wis="3"
                     data-cha="1"></abilities-block>

    <property-line>
      <h4>Damage Immunities</h4>
      <p>poison, psychic</p>
    </property-line>
    <property-line>
      <h4>Condition Immunities</h4>
      <p>blinded, charmed, deafened, exhaustion, frightened, paralyzed,
        petrified, poisoned</p>
    </property-line>
    <property-line>
      <h4>Senses</h4>
      <p>blindsight 60 ft. (blind beyond this radius), passive Perception 6</p>
    </property-line>
    <property-line>
      <h4>Languages</h4>
      <p>—</p>
    </property-line>
    <property-line>
      <h4>Challenge</h4>
      <p>1 (200 XP)</p>
    </property-line>
  </top-stats>

  <property-block>
    <h4>Antimagic Susceptibility.</h4>
    <p>The armor is incapacitated while in the area of an <i>antimagic
      field</i>.  If targeted by <i>dispel magic</i>, the armor must succeed
      on a Constitution saving throw against the caster’s spell save DC or
      fall unconscious for 1 minute.</p>
  </property-block>
  <property-block>
    <h4>False Appearance.</h4>
    <p>While the armor remains motionless, it is indistinguishable from a
      normal suit of armor.</p>
  </property-block>

  <h3>Actions</h3>

  <property-block>
    <h4>Multiattack.</h4>
    <p>The armor makes two melee attacks.</p>
  </property-block>

  <property-block>
    <h4>Slam.</h4>
    <p><i>Melee Weapon Attack:</i> +4 to hit, reach 5 ft., one target.
      <i>Hit:</i> 5 (1d6 + 2) bludgeoning damage.</p>
  </property-block>
</stat-block>
```

The example text is copyright Wizards of the Coast; they make it [available for
free on their website][wotc-basic] through the D&D 5E Basic Rules (it's in the
[DM supplement][dm-basic]).

Visual differences from the MM statblocks
-----------------------------------------

Unfortunately this statblock isn't _quite_ pixel-perfect with regards to the
statblocks in the MM. The differences are:

- **Different typefaces used.** I don't know what typeface is used in the MM,
  and even if I did, I doubt it's available for free from Google Fonts.
- **No textured background.** Obviously, I don't have access to the original
  textures WotC used. Even if I did, I'm not sure I'd use them since that would
  mean serving images which I wanted to avoid (scaling/resolution/deployment
  issues etc).
- **No textured block border.** Same as above.

There are probably other differences as well but I haven't noticed them. I tried
to stick as close to the original as reasonably possible; for instance, I spent
_waaay_ too much time getting the drop-shadow to be the "correct" shade of
brown and the tapered horizontal rule to render _just_ right. _Why?_ Because I
had nothing better to do and it was fun! :)


FAQ
---

### Is there a single-file version?

The [`demo.html`][demo] file in the repository HTML-imports the other HTML
source files. There's also [`demo-inlined.html`][demo-inline] which renders
exactly the same but has all the HTML-imports inlined directly into the
document.

The Python script that produces the inlined version [is also
available][inline-script].

### Why aren't you using polyfills?

While polyfills for Web Components [do exist][platform], they're not perfect and
require a preprocessing stage that inlines all HTML imports and rewrites the new
CSS selectors like `:host`, `::content`, `/deep/` etc. There's no easy way to
tie all this together and frankly, I don't care enough since I'll personally
only use this for locally hosted pages rendered in Chrome.

If someone wants to do the required work to implement the whole preprocessing
pipeline, pull requests are welcome.

License
-------

This software is licensed under the [Apache License, Version 2.0][apache2].

[web-components]: http://webcomponents.org/
[html-import]: http://w3c.github.io/webcomponents/spec/imports/
[custom-elements]: http://w3c.github.io/webcomponents/spec/custom/
[template]: https://html.spec.whatwg.org/multipage/scripting.html#the-template-element
[shadow-dom]: http://w3c.github.io/webcomponents/spec/shadow/
[wc-status]: http://jonrimmer.github.io/are-we-componentized-yet/
[wotc-basic]: http://dnd.wizards.com/articles/features/basicrules?x=dnd/basicrules
[dm-basic]: http://media.wizards.com/2014/downloads/dnd/DMDnDBasicRules_v0.1.pdf
[apache2]: http://www.apache.org/licenses/LICENSE-2.0.html
[platform]: https://www.polymer-project.org/docs/start/platform.html
[demo]: http://valloric.github.io/statblock5e/demo.html
[demo-inline]: http://valloric.github.io/statblock5e/demo-inlined.html
[inline-script]: https://github.com/Valloric/statblock5e/blob/master/tools/inline-imports.py
