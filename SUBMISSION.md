## Submission Notes

### Overall
This was a fantastic challenge. I had never worked with Vue.js before, so learning about using the components and how/when
data updates took me a bit, but Vue's documentation was clear enough for me to learn everything I needed
for this challenge.

### Packages added
- Bootstrap - This cleaned up all of the styling pretty quickly. Threw some containers around some of the components
and things were nicely centered and looked alot better.
  
- jquery/popper.js/portal-vue - required for bootstrap-vue
- bootstrap-vue - Used for the modal for updating/deleting a plane status. Their documentation helped tremendously when
figuring out how to work with Vue.
  
### Difficulties

1. Populating the inputs in the modal. 
    - The modal was a child component of the dashboard, so I had to figure out how to
pass the clicked plane object information into the child component. It took me awhile to realize when the props were being 
      shared with the child component and that I needed to add a :key to get the component to rerender.
      
2. Figuring out the scope of functions.
    - It almost goes hand in hand with understanding where and when props get sent down to child components, but understanding 
    which functions were where and how to call them took some time. Templating my functions for update/delete based off of the 
      read/create functions already there helped in figuring this out.
