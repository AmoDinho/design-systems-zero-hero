# design-systems-zero-hero
My blog post and talk on Design Systems

A link to the talk can be found [here](https://www.figma.com/proto/KedEPuWZk0CXWWNAEf806cOZ/GOA?node-id=1692%3A35&scaling=scale-down)


# Blog Post WIP!!

Since round about the same time last year I've been trying to get my deisgn systems game up to stracth. In this post I'm gonna walk you through how I built two design systems and made component libraries in Vue and React. If you follow along you could also build yours in no time at all. However the outputs are really bare bones and the goal is to get your design system out in the wild to be used in your apps and marketing activities. 


## why do design systems exist? 

Design systems exist purely because they help companies provide a consistent brand and user experince for their products or services. 

Your users are everywhere your brand is. Web, mobile, print, film and clothing are just a few places where your customers/users interat with your brand.

Design systems help bridge the gap between these diffferent platforms and give your team guidelines on how to execute the design and brand.

## how can they improve my ability

### Proptype faster

When building out stuff you want to make sure that you're able to make sure your business requirements are sound. So when making hifidelity prototypes the cognitive load of managing the styling of your app and still making sure the use cases are valid can really eat you up. 

So lets take a look at this file:

[ADD SCREENSHOOTS FROM THREE USE CASES IN FIGMA]

This took me about 30mins to do, while looking over a use case that has three different alternative steps. Because I was able to easliy drag and drop components willy nilly I was able to focus on business requirements and get approval from stakeholders.


### Avoid sharing code between components

At Pimp My Book where I work, we have a bursary app called GOA which helps bursary students order their educational materials and aids bursaries to cut down on wastage. So I had initally made a landing page in Vue, then a month later I needed a tool to help me with documentation for the app. So I use Gridsome, when starting on the docs site I was copying and pasting code between projects. It was really ugly and painful, but I did not have the time to stop and make a lib at the time.

## Phases of building them

So I went through two phases: design and engineering

Out of the design phase you need to come out with a UI Kit in a design tool of your choice, while in the engineering phase you need a component library packaged for your platform. 

### Overview of design phase
I'm a bit of a one man team at the moment. So it is not smart to over design in this phase but rather keep things simple. If you're in a larger team I would still recommend that you try to keep this stage simple and make sure engineers are particpaing in your plans for what the components will look like. Because you could come up with a design that your enigneering team might not know how to pull off and it will just take longer for the components to be shipped because they now have to go out of their to figure out how to bring your over deisigned components to life. 

### Design tools: choose one

When it comes to design tools, it is easy to get overwhelmed. So I will make the decision for you! FIGMA is the only way!

There are tonnes of tools which can be looked at here [insert link to deisgn tools]. 

Why Figma

It is free, you have all the serious functionality to be productive without needing to fork out moneny. 

It is primarily based on the web so it solves accessibility problems without needing to have certain OS or device. 

Neat advanced features like local styles and access to your components. [Supply links to videos of local styles etc]

### Use premade components
If you are sitting in your tool and making components from scrtach like making a rectangle and adding widths, border radius etc then you're a wasteman/wastewoman. Time is precious, use premade UI libraries and then customize everything according to your colours and typography. 

I've been using this template and it is extremly useful. [pdkit.co]

### Focus on colours & typography

Once you set your colours and typography you are on the road to success. Simple go onto Dribbble or Pintrest and search for UI's you like and steal their colour palette. You need to have at least two base colours and accents. So If we look at GOA's DS, I have Green, then I go about two shades darker and two shades lighter. Then do the same for your accents, which will always be Yellow, blue, red, white and grey. For palettes go  to coolours or colourhunt.

For your typography simply take Two fonts from Google Fonts, One for headings and the other for your body text. Then have Five or Six main headings, Then have a body text, caption text. Most importanly, systemize your sizing for your fonts and also spacing. [Add picture of sizing]

 ### Shouldn’t take more than five days
During this design phase, it should not take longer than a working week to get the UI library functional for you to build high fidelity mockups. 

Our goal by doing this is to insure that you're able to ship your project faster because keystake holders might not be able to detect tanigble progress in your project. Trust I'm speaking from first hand experince. 




### Overview of engineering  phase

So now you've done with the designing things. We get to bring our babies to life. 

### Choose framework

I've shipped two component libraries for different projects written in Vue and React. I can't say I have a favourite but the reasoning behind it is that I like doing more complicated apps with React and ligthweight apps with Vue.

So choose either one and you should good to go.

###  Choose CSS framework

So I've opted to use TailwindCSS for both my projects. This is because it allows me complete control over theming and the use of utility classes. Which means I can ditch BEM and Styled Components altogether.

Personally I do not like overwriting existing styles from other UI libraries. This usually has me inspecting the dev tools etc just to change a colour. However, for complex components like accordians etc just import that specific component and take a hit with styling. 
### Component viewer
So when building the component library, you can't structure it like you would a normal web app. This means no routing or anything. You need to figure out how to export all your components and register it with your framework. [Insert examples]

Then once that is done you need to a component viewer that allows you to refresh and view all your components as you are building them. 

### CI/CD + Publishing

Initial when you start building the library, I started with trying to get the simplest component to NPM and verifiying it works by installing in a CodeSandbox app. 

To publish to NPM you just need to :

1. sign up for an account
2. generate a token for your application

So what I did was first deploy locally from my machine by using `npm publish`. First make sure you are logged into your account by using the `npm login` account. Then NPM will take care of the rest.

Before I go over CI/CD lets just touch over my workflow.

- create a branch for the component, eg: feature/dropdown
 - Write a test case for my component. Here I basically state what its functionality needs to be. 
 - Create the component file: eg `Dropdown.vue` and I would add a plan native HTML <select> tag.
 - Then create a `Dropdown.story.js` file to make sure the Storybook server can pick it up. 
 - Then I would go out building the component till it matches the designs in my design system in Figma and has the desired functionality. 
 - Once I'm happy with that I start finishing up my test and make sure it passes locally.
 - Then start merging the PR, Travis is linked to my repo and it will run all my other tests to make sure I've not introduced any bugs while editing any of te other components.
 - Once the Tests are done I merge with master and travis then will publish to NPM on my behalf.

 So Continous Integration/Continous Development is the practice of being able to easily add new code to you codebase without breaking or introducing new bugs into the codebase, while being able to deploy new code frequently and often. As well as automating the deployment process and tests.

 (might not be accurate but this is how I understand it and implement it)

 For deployment tools: Travis, CircleCI, Jenkins, Seed and others are avaiable.

 At work I use Travis for NPM libraries and Seed for my Lambdas. While I use the CI baked into Netlify for my frontends. 

 These deployment tools are therre to help us not constantly type in build commands in out terminals everytime we want to ship something. So with Travis I just need to create a `travis.yml` file and then give it an encrypted token from NPM. I used this blog post on how to figure out how to deploy to NPM. [Link blog post]

 tl;dr

 Basically:

 - grab colours and typography
 - use an existing UI tool kit in your design tool of choice
 - customize the kit according to your brand and make all the components you need to achieve the UX you desire.
 - Start with a typography component in your web framework of choice.
 - deploy to NPM to verify everything is sound.
 - Set up CI/CD + testing 
 - Then build out each component one by one with unit tests. Basically every PR should be a new component added to the library for a user to use.
 - Repeat the cycle till all your required components are done.