# [A11Y](https://web.dev/accessible/what-is-accessibility) notes

Learnings from Google's [web.dev](https://web.dev/) initiative.

## A11Y intro

As a webdeveloper it is my responsibility to help users getting access to the content I build an app around.
Therefore, users with limited accessibility need to be assisted.

In order to assist those users, a site needs a11y principles applied. These vary as such: / control
* Auditory
  * Helping users that have difficulty hearing certain frequencies
  
  
Not all of these principles are applied easily, and some may cost a lot of time to implement and even more to maintain.
Use the A11Y principles wisely.

## A11Y high-level spectrum overview

* Vision
  * Helping users that have limited visibility by using high-contrast colors
  * Using large enough fonts and enable the possibility of increasing those
  * Helping a user that has limited or no visibility with the use of screen-readers
  * Describe the meaning of control elements
  * Describe visual representations such as images and graphs
* Motor / Dexterity
  * Helping users that have limited dexterity by making navigation available through the keyboard
  * Enable voice access
* Auditory
  * Helping users that cannot hear by adding subtitles to video's
  * Helping users that have difficulty hearing by adding captions to audio
  * Helping users that have difficulty hearing by transscripting electronic speech
* Cognitive
  * Helping a wide range of users with different difficulties by removing intrusive distractions from pages
  * Helping users by minimizing flickering and moving parts that are not improving the users experience
  * Removing excessive animations that shift the users context in an unexpected way
  * Help users prevent headaches and improve readability by enabling custom styles
  

# Keyboard access fundamentals

Users with temporary or permanent motor impairments cannot always use a mouse or touch interface.
To allow those users access to your content, a good strategy is to use keyboard navigation.

# Focus and the tab order

A focused element is the element the user is currently interacting with. That might be any input element, button or link.

To move the focus on a page, the user presses <kbd>tab</kbd> to navigate forward, 
or <kbd>shift</kbd>+<kbd>tab</kbd> to navigate backwards.
The currently focused element is often indicated by a **focus ring**, and various browsers style their focus rings differently.
The order in which focus proceeds forward and backward through interactive elements is called the **tab order**.

Elements that are natively interactable are implicitly focusable. They are automatically inserted into the tab order.
The tab order is then automatically set to be the same as the position in the DOM. 
These elements also have native keyboard event-handling. Other elements don't have keyboard handling and are not implicitly focusable.

Implementing a logical tab order is an important part of providing your users with a smooth keyboard navigation experience.
There are two main concepts when asserting your tab order:

* Arrange elements in the DOM to be in logical order
* Correctly set the visibility of offscreen content that should not receive focus

## Arrange elements in the DOM to be in logical order

To check if your applications tab order is logical, you can tab through your page.
Usually focus should follow reading order, left to right and top to bottom.

If the focus order seems illogical, rearrange the elements in the DOM to make it more natural.
If you want something to appear visually earlier on the screen, try moving it **before the elements that come after it**.

| Logical tab order            | Illogical tab order                          |
|------------------------------|----------------------------------------------|
| `<button>Kiwi</button>`      | `<button style="float: right">Kiwi</button>` |
| `<button>Peach</button>`     | `<button>Peach</button>`                     |
| `<button>Coconut</button>`   | `<button>Coconut</button>`                   |

If you change a button or other element's position with CSS, keep in mind the tab order remains to be the DOM order.

## Correctly set the visibility of offscreen content

Sometimes offscreen interactive elements need to be in the dom but not in the tab order.
If you have a sidebar navigation that collapses, the user should not be able to tab through them. That makes no sense.
To prevent the element from receiving focus, give the element either of the following CSS properties:

* `display: none;`
* `visibility: hidden;`

The above also works on parent elements. These all work:

```
<div style=display:none>
  <button>a</button>
</div>

<button style="visibility: hidden">b</button>
<button style="display:none">c</button>
```
To add the element back into tab order, for example when the navigation is opened, replace the above properties with:

* `display: block;`
* `visibility: visible;`

:information_source: To get the element that is focussed in javascript, use the `document.activeElement` property.
