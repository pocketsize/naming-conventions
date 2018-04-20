# Pocketsize Naming Conventions

Base rule: `{block}-{element} [is/has]-{modifier}`

The block part of the class should describe the scope.
The element part of the class should describe what the element is.
Only the modifier class can describe what the element looks like.

When you need to add another element in your mark-up for styling purposes that serves no purpose without the element it's wrapping or contained within it should be named as follows:
* `{block}-{element}-outer` for outer elements
* `{block}-{element}-inner` for inner elements

## Examples

Here are a couple of code examples.

### HTML

```html
<section class="page">
	<div class="page-inner">
		<h2 class="page-title">The Title</h2>

		<div class="page-content">
			<!-- begin classless content (usually from cms or other data source) -->
			<p>Here's the content. This is a paragraph and below is a list.</p>
	
			<ul>
				<li>List item 1</li>
				<li>List item 2</li>
				<li>List item 3</li>
			</ul>
			<!-- end classless content -->
		</div>

		<div class="page-links">
			<div class="page-link-outer">
				<a href="#" class="page-link">A link</a>
			</div>
		</div>
		
		<div class="page-social-icons">
			<div class="page-social-icon-outer">
				<a class="page-social-icon is-facebook" href="https://www.facebook.com"></a>
			</div>
			<div class="page-social-icon-outer">
				<a class="page-social-icon is-instagram" href="https://www.instagram.com"></a>
			</div>
		</div>
	</div>
</section>
```

### SCSS

Apart from the Bolts reset, we do not write global styles. For common styles we create shadow classes that we extend on the relevant elements in each block scope.

```scss
%title { font-weight: 700; }

%title-primary {
	@extend %title;
	font-size: 2em;
}

%title-secondary {
	@extend %title;
	font-size: 1.5em;
}

p, ul {
	%wysiwyg & + & { margin-top: 1em; }
}

%wysiwyg {
	p, li { line-height: 1.6; }
}

section.page {
	.page-inner { @include container; }

	.page-title { @extend %title-primary; }

	.page-content { @extend %wysiwyg; }
	
	.page-links-title { @extend &title-secondary; }
	
	.page-links {
		@include inline-layout(20px);
	}
	
	.page-link-outer {
		@media ( width-to(medium) ) { width: 50%; }
		@media ( width-from(medium) ) { width: 25%; }
	}
	
	.page-link {
		display: inline-block;

		&:hover { text-decoration: underline; }
	}

	.page-social-icons-title { @extend &title-secondary; }

	.page-social-icons { @include inline-layout(10px); }

	.page-social-icon {
		display: block;
		width: 20px;
		height: 20px;

		&.is-facebook { @include background('../images/facebook.png'); }
		&.is-instagram { @include background('../images/instagram.png'); }
	}
}
```

#### Indentation

We indent using tabs in the first level. To align "columns" we use spaces. We don't mix tabs and spaces.
