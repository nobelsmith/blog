---
title: "I Tried Next.js (and its my new guilty pleasure)"
date: 2025-05-05T22:08:25-05:00
draft: false
categories: ["Tech"]
tags: ["software development", "programming", "full-stack", "Next.js"]
---

As a developer constantly exploring new frameworks and tools, I've always been curious about Next.js but never quite found the time to dive in properly. When Next.js 15 was released and I started to see the rising popularity of server-side components, I finally decided it was time to take the plunge. I have previously dabbled in Sveltekit and I have done my time in JQuery and PHP, but I would not have considered myself a frontend or full stack developer before undertaking this project.

## My Journey Into Next.js

My background is primarily in backend development and database administration. I know several programming languages with go and python being my favorite, but I do not even write any Typescript/Javascript in my day job. This bit of information could leave you wondering why I decided to try Next.js as opposed to something tried and true like flask or sexy like templ and htmx. Truth be told I have started down those rabbit holes before, and as much as my heart wanted to believe in a future where we go back to web servers putting together the HTML and sending it as api responses I don't think that is going to happen. There is too much magic that needs to happen on the front end nowadays to not include JS in your project, and if I am going to have to include it I have come to the conclusion that it is best to fully commit. With Next.js server components my dreams are coming true in ill be it a different way than I would have imagined.

The first thing that struck me was how seamlessly Next.js 15 integrates what would normally be complex features:

- The App Router provides an intuitive file-system based routing
- Server Components allow for reduced client-side JavaScript
- Server Actions simplify form handling without API endpoints
- The new Turbopack offers lightning-fast development experience
- Layout files and app groups for organization and styling

The next thing I was shocked by was how many fanstastic tools are out there for the Next.js/React ecosystem:

- Shadcn components allow you to own your code while ensuring consistent styling
- Tailwind CSS allows for easy modifications to ui components
- Auth.js exposes numerous providers and fantastic session management options
- Drizzle ORM for simple database operations

What began as a simple experiment quickly evolved into a full-fledged project as I found myself eagerly implementing features just to see how Next.js would handle them.

## Technical Deep Dive

### The App Router: A Game Changer

The App Router in Next.js 15 represents a paradigm shift in how we structure web applications. Unlike the older Pages Router, the App Router follows a more intuitive nested layout approach:

```jsx
// app/layout.js - Root layout
export default function RootLayout({ children }) {
  return (
    <html lang="en">
      <body>{children}</body>
    </html>
  );
}

// app/blog/layout.js - Blog section layout
export default function BlogLayout({ children }) {
  return (
    <section>
      <nav>Blog Navigation</nav>
      {children}
    </section>
  );
}
```

This structure immediately felt more natural than the old create-react-app Pages router. I enjoy file-based routing, and the component model makes writing reusable components extremely simple.

### Server Components: Less JavaScript, More Performance

One of the most impressive features in Next.js 15 is the default Server Components. These components render on the server, sending only the HTML to the client (as god intended), which translates to:

- Smaller bundle sizes
- Faster page loads
- Improved SEO
- Better performance on mobile devices
- Data fetching happens securely on the server

The syntax for creating Server Components is deceptively simple - they're just regular React components by default. The magic happens behind the scenes:

```jsx
// This component renders on the server by default
"use server";
export default async function BlogPosts() {
  // This data fetching happens on the server
  const posts = await fetchPosts();

  return (
    <div>
      {posts.map((post) => (
        <article key={post.id}>
          <h2>{post.title}</h2>
          <p>{post.excerpt}</p>
        </article>
      ))}
    </div>
  );
}
```

What blew me away was how this eliminated so many of the data-fetching headaches I'd faced in traditional React apps. No more api requests appearing in users network tabs, no more loading states, no more useEffect fetch calls, no more state management for API data - it just works.

### Server Actions: Forms Without the Fuss

Server Actions in Next.js 15 feel like something that should have existed years ago. They allow you to write server-side functions that can be called directly from your components. This was one of my favorite things about SvelteKit and I was so happy to see it similarly implemented here:

```jsx
export default function ContactForm() {
  async function submitForm(formData) {
    "use server";
    // Server-side code here
    const name = formData.get("name");
    const email = formData.get("email");
    await saveContactToDatabase({ name, email });
  }

  return (
    <form action={submitForm}>
      <input name="name" />
      <input name="email" type="email" />
      <button type="submit">Submit</button>
    </form>
  );
}
```

This simple `'use server'` directive completely changes the game. No more setting up API endpoints, no more complex state management for form submission - the boundary between client and server code becomes almost invisible.

## Real-World Application

To truly test Next.js 15, I built two projects. One was a brand new idea, and one I had written in SvelteKit previously. The difference was night and day:

1. **Development Experience**: Hot reloading was noticeably faster with Turbopack, making iteration cycles shorter
2. **Performance**: Initial load times decreased by nearly 60% thanks to Server Components
3. **Code Organization**: The App Router encouraged a more logical project structure
4. **Feature Implementation**: Features that would have taken days to implement (like authentication with protected routes) took mere hours
5. **Available Information**: I never had to reinvent the wheel any problem I encountered had already been solved by the Community
6. **Tooling**: Not having to import the sketchy Svelte port of a react library is such an improvement
   The most significant advantage was the dramatic reduction in boilerplate code. With Next.js handling routing, server-side rendering, and data fetching so elegantly, I could focus on the actual business logic and user experience.

## The Challenges

Despite my newfound enthusiasm, Next.js 15 isn't without its learning curves:

- **Mental Model Shift**: Understanding when code runs on the server versus the client takes time
- **Documentation Gaps**: While vastly improved, some newer features still lack comprehensive examples (Especially since I was using Auth.js or NextAuth beta)
- **TypesScript Support**: Sometimes I wanted to use libraries that did not come with types and that caused many issues.
- **Build Process**: The build errors can become overwhelming especially if you are not frequently building as those errors are suppressed during development

These challenges were far outweighed by the benefits, but they're worth noting for anyone considering making the switch.

## Is Next.js 15 Right for You?

After spending significant time with Next.js 15, here's my assessment of who would benefit most:

### Perfect For:

- Teams building content-heavy websites where SEO matters
- Developers tired of reinventing routing and data fetching solutions
- Projects that need to balance performance with developer experience
- Applications requiring both static and dynamic content

### Perhaps Less Ideal For:

- Extremely simple single-page applications
- Projects that only deal in static content (like this one!)
- Projects with very specific custom server requirements
- Teams deeply invested in other meta-frameworks with similar features (Im talking to you PHP Devs just keep on keeping on)

## Final Thoughts

What started as a weekend exploration has fundamentally changed how I approach web development. Next.js 15 manages to deliver on its promises of simplifying complex web development challenges while maintaining the flexibility that made React popular in the first place.

Is it perfect? No. Is it my new guilty pleasure that I can't stop recommending to fellow developers? Absolutely.

If you're on the fence about trying Next.js 15, consider this your sign to give it a shot. You may feel rad like the Svelte stans or demure like the Laravel web artisans, but you will get work done!

## Getting Started Tips

If you're inspired to try Next.js 15 yourself, here are some tips to get you started:

1. **Start Fresh**: Begin with a new project using `npx create-next-app@latest` rather than migrating existing code
2. **Embrace Server Components**: Default to Server Components and only use Client Components when needed
3. **Use the App Router**: Take time to understand the routing conventions
4. **Read the Docs**: The official Next.js documentation has greatly improved and offers excellent guidance
5. **Join the Community**: The Next.js Discord and GitHub discussions are fantastic resources for troubleshooting
6. **Ask ChatGPT**: These new models have seen so much react that they almost always give you reasonable answers

After all of this glazing you may find it shocking, but this site is not actually written in Next.js! I am a firm believer that no matter how good a tool is you should always take a moment to consider if it is actually the best tool for the job. In my next post I will be outlining what technology I chose to build this site in and why so stay tuned!
