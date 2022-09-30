# be-matching [TODO]

React to DOM elements coming and going

## Example 1

```html
<div itemscope itemtype="https://schema.org/Movie">
  <h1 itemprop="name">Avatar</h1>
  <span>Director: <span itemprop="director">James Cameron</span> (born August 16,
    1954)</span>
  <span itemprop="genre">Science fiction</span>
  <a href="https://youtu.be/0AY1XIkX7bY" itemprop="trailer">Trailer</a>
</div>
<script nomodule be-matching=*[itemprop]>
    console.log(target, added);
    target.contentEditable = added;
</script>
```

logs all elements from previous sibling with attribute itemprop.  makes them editable

is shorthand for:

```html
<div itemscope itemtype="https://schema.org/Movie">
  <h1 itemprop="name">Avatar</h1>
  <span>Director: <span itemprop="director">James Cameron</span> (born August 16,
    1954)</span>
  <span itemprop="genre">Science fiction</span>
  <a href="https://youtu.be/0AY1XIkX7bY" itemprop="trailer">Trailer</a>
</div>
<script nomodule be-exporting be-matching='{
    "for": "*[itemprop]",
    "scope": ["upSearch", ":not(script)"],
}'>
    export const handler = ({target, added, }) => {
        console.log(target, added);
        target.contentEditable = added;
    };
</script>
```

piggy backs on be-vigilant, but value-add is linkage to handler 

## Example 2

```html
<div itemscope itemtype="https://schema.org/Movie">
  <h1 itemprop="name">Avatar</h1>
  <span>Director: <span itemprop="director">James Cameron</span> (born August 16,
    1954)</span>
  <span itemprop="genre">Science fiction</span>
  <a href="https://youtu.be/0AY1XIkX7bY" itemprop="trailer">Trailer</a>
</div>
<script nomodule be-matching=itempropAttrs>
    console.log({target, val, scope});
</script>
```

val is the value of the itemprop attribute.  Works as long as the last capital letter is an A, ends with s.

scope is the matched element found based on the scope query.  The preceding div in this case.

And scope has some utility added to it:

scope.itemprops() return {
  genre: 'Science fiction',

}

actually, a proxy

scope.itemprops({genre: null, director: null}) = {
  genre: 'Science fiction',
  director: 'James Cameron'
}

actually it's a ProxyBag with EventTarget


