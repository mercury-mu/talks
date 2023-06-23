---
layout: cover
highlighter: shiki
monaco: true
fonts: Sora
info: |
  ## Mastering Business Innovation

  Learn to build fast with the right tools

  [Bruno Bernard](https://twitter.com/unkaimaster) at [Frontend.mu 2023](https://frontend.mu/meetup/45)
  [Jordan Bienvenue](https://twitter.com/unkaibuilder) at [Frontend.mu 2023](https://frontend.mu/meetup/45)

---

# Build Fast With The Right Tools

Shadcn UI/Prisma/tRPC in NextJS

<div class="uppercase text-sm tracking-widest">
Bruno Bernard
</div>

<div class="uppercase text-sm tracking-widest">
Jordan Bienvenue
</div>

<div class="abs-bl mx-14 my-12 flex">
  <img src="https://avatars.githubusercontent.com/u/137558017?s=96&v=4" class="h-8">
  <div class="ml-3 flex flex-col text-left">
    <div><b>Mercury</b> Innovation</div>
    <div class="text-sm opacity-50">Jun. 24th, 2023</div>
  </div>
</div>


---
layout: 'intro'
---

# Jordan Bienvenue
React Developer | Web3 | Drone Pilot

<div class="leading-8 opacity-80">
CEO & Co-Founder of <b>Mercury Innovations</b><br>
COO & Co-Founder of <b>UNKAI Labs</b><br>
Owner of Bees
</div>

<div class="my-10 grid grid-cols-[40px_1fr] w-min gap-y-4">
  <ri-github-line class="opacity-50"/>
  <div><a href="https://github.com/jordanbienvenue" target="_blank">jordanbienvenue</a></div>
  <ri-twitter-line class="opacity-50"/>
  <div><a href="https://twitter.com/unkaibuilder" target="_blank">UNKAIBuilder</a></div>
  <ri-user-3-line class="opacity-50"/>
  <div><a href="https://jordanbienvenue.com" target="_blank">jordanbienvenue.com</a></div>
</div>

<img src="https://avatars.githubusercontent.com/u/17847357?v=4" class="rounded-full w-40 abs-tr mt-16 mr-12"/>
<img src="img/qr-jordan.png" class="rounded-5 w-40 abs-tr mt-80 mr-12"/>


---
layout: 'intro'
---

# Bruno Bernard
Consultant | Web3 & Open Source | Hodophile


<div class="leading-8 opacity-80">
CTO & Co-Founder of <b>Mercury Innovations</b><br>
CTO & Co-Founder of <b>UNKAI Labs</b><br>
Owner of <b>Ti Point Technologies</b><br>
</div>

<div class="my-10 grid grid-cols-[40px_1fr] w-min gap-y-4">
  <ri-github-line class="opacity-50"/>
  <div><a href="https://github.com/eznix86" target="_blank">eznix86</a></div>
  <ri-twitter-line class="opacity-50"/>
  <div><a href="https://twitter.com/unkaimaster" target="_blank">UNKAIMaster</a></div>
</div>

<img src="https://avatars.githubusercontent.com/u/26553194?v=4" class="rounded-full w-40 abs-tr mt-16 mr-12"/>
<img src="img/qr-bruno.png" class="rounded-5 w-40 abs-tr mt-80 mr-12"/>

---
layout: center
---

# Shadcn UI/Prisma/tRPC in NextJS


---
layout: image-right
image: ./img/calx.mu.png
---

# Introducing Calx.mu

- NextJS
- Shadcn UI
- tRPC
- Prisma


---
layout: center
---

# Reasons
<img src="https://i.imgflip.com/60zo0i.jpg" alt="speed"> 


---
layout: center
---

# Let's dive into each tech

<img src="https://miro.medium.com/v2/resize:fit:651/1*rf4QAy4yYPdfuLsZ7NrHZA.jpeg" alt="meme"> 


---
layout: center
---

# Shadcn UI

 ...


---
layout: center
---

# Shadcn UI Benefits

 ...


---
layout: center
---

# Speed for the backend too

---
layout: intro
---

# Why Prisma and tRPC

- Typescript
- type-safety
- ...Autocompletion



---
---

# Prisma

- ORM
- Type-safety
- Nice Workflow

---
---

# Prisma Schema

Get Autocompletion with VSCode Integration

- Schema Model

```prisma
model User {
  id    Int     @id @default(autoincrement())
  email String  @unique
  name  String?
  posts Post[]
}
```

- Model Ready with ORM Capability

```ts
// no more: select * from users
const users = await prisma.user.findMany() 
//     ^----- this returns an object user in typescript `Users[]`
```

---
layout: image-right
image: https://i.imgflip.com/3u0cu2.jpg
---

# Talking to the Frontend

Which is more flexible ?

- API ?
- GraphQL ?
- tRPC ?

---
---

# REST API
- Paths ? Methods? 
- No type-safety
- Changes - JSON update / Endpoint update = Break

```
GET /users/bookings ?
POST /bookings ?
```

```ts
  const response = await fetch('/users');

  if (!response.ok) {
      // ^----- What about other states, loading, errors, pending ?

    const message = `An error has occured: ${response.status}`;
    throw new Error(message);
  }

  const users = await response.json();
  //    ^----- Well I get users. But what's inside

  // :( NO! not console.log again
  console.log(users)

```

---
---

# GraphQL
- Solve what API problems, but at what cost ?
- But more complex ?
  - More boilerplate code to write
- Bundle size: 40kb ? 
- Need to write boilerplate again in the front
  - Does your frontend dev know GraphQL?
  - String ? Are you serious ?

---
---

# GraphQL Mess Contemplation
Even the code goes outside the screen. lol.
No bashing. Just look.

```ts
// On the server
export const User = objectType({
  name: 'User',
  description: 'A User',
  definition(t) {
    t.nonNull.id('id');
    t.nonNull.date('createdAt');
    t.nonNull.date('updatedAt');
    t.nonNull.list.nonNull.field('roles', { type: 'Role' });

    // Show email as null for unauthorized users
    t.string('email', {
      resolve: (profile, _args, ctx) => (canAccess(profile, ctx) ? profile.email : null),
    });
  },
});

// On the client.
export const QUERY = gql`
  query User($id:ID!) {
    user(id:$id) {
      name
    }
  }
`;

export const UserCell = ({userId}:{userId:string}) => {
	const { data, loading, error } = useUserQuery({
    variables: {
      where: { id: userId },
    },
  });

  // ...
}
```


---
layout: center
---

# Introducing tRPC

:)

---
---

# tRPC on the backend

- Endpoint Out Of The Box
- Validation with Zod
- Type-safety Complete

```ts
// backend
import { z } from 'zod';
 
const appRouter = router({
  userById: publicProcedure
    .input(z.string()) // validation
    .query(async (opts) => { // return what you need to return
      const { input } = opts;
      // Retrieve the user with the given ID
      const user = await user.findById(input);
      //     ^------- this is prisma, remember type-safety !
      return user; // Oh we got an object.
    }),
});
```

---
---

# tRPC on the frontend

- Autocomplete

```ts
const user = await trpc.userById.query('1');
//     ^------- type-safety

```

- States with React Query built-in

```ts
import { trpc } from '../utils/trpc';

export function MyComponent() {
  const mutation = trpc.login.useMutation();
  //... call handleLogin
  return (
    <div>
      {mutation.isSuccess ? <div>Logged In</div> : null}  
      //.. button
      {mutation.error && <p>Something went wrong! {mutation.error.message}</p>}
      {mutation.isLoading && <Spinner/>}
    </div>
  );
}

```

---
---

# Recap

- Prisma gives 
  - a better DX
  - Workflow for migration and type-safety
- tRPC
  - No endpoints
  - Use the power of your IDE
  - Give your states


---
---

# Where and When can I use it ?
- It is good for monorepo/full-stack environment
  - Where frontend & Backend is very close.
- NextJS is a good way to start using it
- Not possible to upload files with it 
  - Supports only `json` payload
  - You can `base64` your file and upload it.
  - See (SST)[http://sst.dev/]

- Maintained by only one dude ([KATT] (https://github.com/KATT))
- Start Today.

---
---

# Questions ?
