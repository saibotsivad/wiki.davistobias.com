---
title: Possible HTML Styles
description: The different ways that I've seen HTML written.
---

I did line wrapping at around 60 characters. In truth most editors will wrap around 100,
but also most HTML will several indentations, so I think doing it this way will
demonstrate some of the wrapping styles better.

Note about `<a>` elements:

If you place child text/element of an `<a>` element on a newline, whitespace is introduced:

```html
<!--
the underline on <a> will extend to the left and right of the <span> and text
   [icon] Title Text
 =====================
-->
<a href="">
	<span class="icon"></span>
	Title Text
</a>
```

Therefore it is sometimes necessary to write the child text/elements to have no space:

```html
<!--
the underline on <a> will only be under the <span> and text
   [icon] Title Text
   =================
-->
<a href=""><span class="icon"></span> Title Text</a>
```

# 0

Everything strung out until it wraps, then indent two tabs.

Children indented one tab.

```html
<div class="dropdown">
	<button type="button" id="dropdownMenu2" data-toggle="dropdown"
			aria-expanded="true"
			class="btn btn-default btn-sm dropdown-toggle">
		Group Actions <span class="caret"></span>
	</button>
	<ul role="menu" class="dropdown-menu">
		<li role="presentation">
			<button role="menuitem" type="submit" name="status"
					value="D" title="Delete Documents"
					class="btn-link">
				<span class="glyphicon glyphicon-trash"></span>
				Delete
			</button>
		</li>
		<li role="presentation">
			<a href="/edit/ID" role="menuitem" name="status" title="Edit Documents"
					class="btn-link"><span class="glyphicon glyphicon-pencil"></span>
			Edit</a>
		</li>
	</ul>
</div>
```

# 1

Only if the attributes are long enough to wrap: Everything after the first attribute
on its own line, indented two tabs.

Children indented one tab.

```html
<div class="dropdown">
	<button type="button"
			id="dropdownMenu2"
			data-toggle="dropdown"
			aria-expanded="true"
			class="btn btn-default btn-sm dropdown-toggle">
		Group Actions <span class="caret"></span>
	</button>
	<ul role="menu" class="dropdown-menu">
		<li role="presentation">
			<button role="menuitem"
					type="submit"
					name="status"
					value="D"
					title="Delete Documents"
					class="btn-link">
				<span class="glyphicon glyphicon-trash"></span>
				Delete
			</button>
		</li>
		<li role="presentation">
			<a href="/edit/ID"
					role="menuitem"
					name="status"
					title="Edit Documents"
					class="btn-link"><span
							class="glyphicon glyphicon-pencil"></span>
			Edit</a>
		</li>
	</ul>
</div>
```

# 2

If there are multiple attributes, even if they wouldn't wrap: Everything after the first attribute
on its own line, indented two tabs.

Children indented one tab.

```html
<div class="dropdown">
	<button type="button"
			id="dropdownMenu2"
			data-toggle="dropdown"
			aria-expanded="true"
			class="btn btn-default btn-sm dropdown-toggle">
		Group Actions <span class="caret"></span>
	</button>
	<ul role="menu"
			class="dropdown-menu">
		<li role="presentation">
			<button role="menuitem"
					type="submit"
					name="status"
					value="D"
					title="Delete Documents"
					class="btn-link">
				<span class="glyphicon glyphicon-trash"></span>
				Delete
			</button>
		</li>
		<li role="presentation">
			<a href="/edit/ID"
					role="menuitem"
					name="status"
					title="Edit Documents"
					class="btn-link"><span
							class="glyphicon glyphicon-pencil"></span>
			Edit</a>
		</li>
	</ul>
</div>
```

# 3

All attributes on their own line, indented two tabs.

Children indented one tab.

```html
<div
		class="dropdown">
	<button
			type="button"
			id="dropdownMenu2"
			data-toggle="dropdown"
			aria-expanded="true"
			class="btn btn-default btn-sm dropdown-toggle">
		Group Actions
		<span
				class="caret">
		</span>
	</button>
	<ul
			role="menu"
			class="dropdown-menu">
		<li
				role="presentation">
			<button
					role="menuitem"
					type="submit"
					name="status"
					value="D"
					title="Delete Documents"
					class="btn-link">
				Delete
			</button>
		</li>
		<li
				role="presentation">
			<a
					href="/edit/ID"
					role="menuitem"
					name="status"
					title="Edit Documents"
					class="btn-link"><span
							class="glyphicon glyphicon-pencil"></span>
			Edit</a>
		</li>
	</ul>
</div>
```

# 4

If attributes wrap, all attributes on their own line, indented one tab.

The right-angle-bracket of the element start is not indented.

The element end is `/>` if no child elements.

Children indented one tab.

```html
<div class="dropdown">
	<button
		type="button"
		id="dropdownMenu2"
		data-toggle="dropdown"
		aria-expanded="true"
		class="btn btn-default btn-sm dropdown-toggle"
	>
		Group Actions
		<span class="caret"></span>
	</button>
	<ul
		role="menu"
		class="dropdown-menu"
	>
		<li role="presentation">
			<button
				role="menuitem"
				type="submit"
				name="status"
				value="D"
				title="Delete Documents"
				class="btn-link"
			>
				Delete
			</button>
		</li>
		<li role="presentation">
			<a
				href="/edit/ID"
				role="menuitem"
				name="status"
				title="Edit Documents"
				class="btn-link"
			><span
				class="glyphicon glyphicon-pencil"
			></span>
				Edit</a>
		</li>
	</ul>
</div>
```
