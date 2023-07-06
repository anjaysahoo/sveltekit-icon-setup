# Setting Up Custom Icons in SvelteKit using Figma

This guide will walk you through the process of setting up custom icons in your SvelteKit project using Figma. This approach allows you the freedom to customize the icons according to your needs, without relying on external libraries that can increase file size.

## Steps

1. Choose a Figma library that contains the icons you want to use in your app. Here are a few example libraries:
    - [Microsoft Fluent System Iconography (Community)](https://www.figma.com/file/01vwi5xNnnl5VskOxJ79VU/Microsoft-Fluent-system-iconography-(Community)?type=design&mode=design&t=8tLR3W60tJvibM2u-7)
    - [Material Design Icons (Community)](https://www.figma.com/file/0vztYVBfcdIxt5tUdFnHW0/Material-Design-Icons-(Community)?type=design&mode=design&t=8tLR3W60tJvibM2u-7)

2. Open the selected Figma library and choose an icon. Export the icon as an SVG file.

3. Open the SVG file and locate the `<path>` tag. Copy the value of the `d` attribute.

4. In your SvelteKit project, create a new file `src/utils/appIcon.ts`. Inside this file, define a constant variable for each icon you want to use. For example:
   ```javascript
   // src/utils/appIcon.ts
   export const search = "M15.5 14H14.71L14.43 13.73C15.41 12.59 16 11.11 16 9.5C16 5.91 13.09 3 9.5 3C5.91 3 3 5.91 3 9.5C3 13.09 5.91 16 9.5 16C11.11 16 12.59 15.41 13.73 14.43L14 14.71V15.5L19 20.49L20.49 19L15.5 14ZM9.5 14C7.01 14 5 11.99 5 9.5C5 7.01 7.01 5 9.5 5C11.99 5 14 7.01 14 9.5C14 11.99 11.99 14 9.5 14Z";
   ```

5. Create a new file `src/lib/Icon.svelte` and paste the following code into it:
   ```html
   <!-- src/lib/Icon.svelte -->
   <script>
       export let color = "#fff";
       export let stroke = color;
       export let filled = true;
       export let fill = filled ? color : 'none';
       export let size = '2em'; // default 1em match the parent element
       export let strokeWidth = 0.1;
       // default heart icon
       export let d = "M4.318 6.318a4.5 4.5 0 000 6.364L12 20.364l7.682-7.682a4.5 4.5 0 00-6.364-6.364L12 7.636l-1.318-1.318a4.5 4.5 0 00-6.364 0z";
  

   </script>

   <svg class="icon" width={size} height={size} viewBox='0 0 24 24' fill="none" xmlns="http://www.w3.org/2000/svg">
       <path {d} {fill} {stroke} stroke-width={strokeWidth}/>
   </svg>

   <style>
       .icon {
           position: relative;
           display: inline-block;
       }
   </style>
   ```

6. Now, you can use the custom icon in any `.svelte` file of your project. Import the `Icon` component and the desired icon from `src/utils/appIcon.ts`, and use the `Icon` component with the desired properties. For example:
   ```html
   <script>
       import Icon from "$lib/Icon.svelte";
       import { search } from "../utils/appIcon";
   </script>

   <Icon d={search} color="red" size="5rem"/>
   ```

   You can customize the `color`, `size`, and other properties of the icon component as needed.

## Reference

For more details on this approach, you can refer to the following article:
- [How to Add Customizable SVG Icons in Svelte.js App](https://javascript.plainenglish.io/how-to-add-customizable-svg-icons-in-svelte-js-app-488648d302c8)
