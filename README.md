## jovian-jobot - day - 1
https://jovian.com/learn/how-to-build-an-ai/lesson/episode-1-first-contact-with-jobot

E1: First Contact with Jobot - How to Build an AI


In the first episode of "How to Build an AI," we embark on exciting journey of building Jobot, a helpful and programmable AI that can be deeply integrated into any software application. We'll guide you through the process, sharing valuable insights and expertise along the way.

The following topics are covered in this tutorial:

Understanding what it takes to build a AI-powered applications

Creating a chatbot UI similar to ChatGPT using React, NextJS & TailwindCSS

Connecting a chatbot UI to the OpenAI API & streaming messages

Deploying a chatbot UI to the cloud using GitHub and Vercel

The best way to learn these skills is to follow along step-by-step and type out all the code yourself.

Problem Statement

PROBLEM: Build & deploy the chat interface shown in the above wireframe with the following features:

An input box where a user can enter a message and send it to Jobot

New messages from the user are sent to the OpenAI ChatGPT API

The response, along with the conversation history is shown above the input box

The user can provide their OpenAI API key in a secure input box in the page header

Prerequisites
The tutorial assumes basic knowledge of the following:

HTML, CSS, and JavaScript

Git, GitHub, and VS Code

ReactJS, NextJS, and Tailwind CSS

Links to beginner-friendly resources for learning these skills are included at the end.

TIP: Try to learn just enough so that you can understand and build on top of the code in this tutorial, and use ChatGPT (or Jobot) for help.

Code & Finished Site
The code for this tutorial can be found here:

Source code: https://github.com/jovianhq/jobot

Finished site: https://jobot.dev

Project Setup
We'll use GitHub for hosting our project and GitHub Codespaces for development.

EXERCISE: Watch this tutorial to learn the basics of Git & GitHub in 45 minutes: https://www.youtube.com/watch?v=tRZGeaHPoaw

Creating a Project Repository

Follow these steps to sign up and create a new repository on GitHub:

Go to GitHub.com and click on the "Sign up" button in the top right corner. Follow the prompts to create a new account by entering your email address, a username, and a password.

After creating your account, you'll be taken to the GitHub dashboard. To create a new repository, click on the "New" button located on the left side of the dashboard.

On the "Create a new repository" page, enter a name for your repository, a brief description, and choose whether you want it to be public or private. If you choose a private repository, you'll need to have a paid GitHub account.

Once you've filled out the necessary information, click on the "Create repository" button to create your new repository.

Now that you've created your repository, you'll be taken to the repository page, where you can add files, make changes to your code, and collaborate with others.

Congratulations! You've successfully signed up for GitHub and created a new repository.

From here, you can start adding files, making changes to your code, and collaborating with others to build your software project. You can do either by downloading the repository to your computer of using a cloud-based development platform like GitHub Codespaces.

EXERCISE: Learn more about the README.md, .gitignore and LICENSE files here:

README.md - https://docs.github.com/en/repositories/managing-your-repositorys-settings-and-features/customizing-your-repository/about-readmes

.gitignore - https://docs.github.com/en/get-started/getting-started-with-git/ignoring-files

LICENSE - https://docs.github.com/en/repositories/managing-your-repositorys-settings-and-features/customizing-your-repository/licensing-a-repository

Starting a GitHub Codespace

Here are the steps to open up a repository in Codespaces and launch it within VS Code:

Navigate to the GitHub repository that you want to work on.

Click on the "Code" button, and select "Open with Codespaces" from the dropdown menu.

Select the Codespace configuration that you want to use, or create a new one if necessary.

Wait for the Codespace to be created, which may take a few minutes, if done for the first time.

Once the Codespace is ready, click on the "Open in Visual Studio Code" button

You can either work with the browser-based version of VS Code, or you can connect remotely to the codespace using your installation of VS Code.

Learn more about using VS Code with Codespaces here: https://code.visualstudio.com/docs/remote/codespaces

NOTE: GitHub provides 120 hours of free codespaces usage for personal accounts. Learn more about the pricing here.

Creating a NextJS Project
NextJS is a popular React framework for building server-rendered applications, static websites, and APIs with a great focus on performance and best practices.

One of the easiest ways to create a new NextJS project is by using the create-next-app CLI tool, which sets up a fully functional, customizable template with minimal effort. Follow these steps:

Run the following command, replacing my-next-app with your desired project name, and follow on-screen instructions configure the project as desired:
npx create-next-app my-next-app
Recommended settings:

✔ Would you like to use TypeScript with this project? No
✔ Would you like to use ESLint with this project? Yes
✔ Would you like to use Tailwind CSS with this project? Yes
✔ Would you like to use `src/` directory with this project? Yes
✔ Would you like to use experimental `app/` directory with this project? No
✔ What import alias would you like configured? @/*
Move into the newly created project folder by running:
cd my-next-app
Run the following command to start the NextJS development server and open it in a new tab via Cmd/Ctrl+Click on the server URL shown on screen (e.g. https://localhost:3000 ):
npm run dev

Browse the src folder using the VS Code sidebar. The project will have a predefined structure, which includes:

pages: This folder contains the application's pages.
public: This folder holds the static assets, such as images and fonts.
styles: This folder contains global and component-specific CSS files.
package.json: This file defines dependencies and scripts for your project.
Clean up the template code by opening up src/pages/index.js and replacing it with the following code:

export default function Home() {
  return <div>Hello world</div>;
}
Clean up the templates styles by opening up src/styles/globals.css and replacing it with the following code:
@tailwind base;
@tailwind components;
@tailwind utilities;

ESLint (syntax error detection tool for JavaScript) needs to be informed about the working directory for the NextJS project. Go to "File" > "Preferences" > "Settings" > "Workspace", search for "eslint working" and click on "Edit in settings.json" and add the jobot-web directory:
{
  "eslint.workingDirectories": ["./jobot-web"]
}
You can now start editing these files and adding your own components to build your application.

EXERCISE: Learn the basics of ReactJS and NextJS in under an hour by following these tutorials:

ReactJS (30 mins) - https://www.youtube.com/watch?v=hQAHSlTtcmY

NextJS (30 mins) - https://www.youtube.com/watch?v=OTuHnVvxTDs

Integration with ChatGPT

ChatGPT, powered by OpenAI, is a large-scale language model that can generate human-like text responses based on a given input. The ChatGPT API provides a convenient way to integrate ChatGPT into your applications, enabling you to leverage its powerful natural language processing capabilities

Navbar & API Key
To use the ChatGPT API, you need to sign up for an API key from OpenAI. Visit the OpenAI platform (https://platform.openai.com/signup/) to create an account and obtain your API key. Keep the API somewhere safe and never share it publicly or add it directly to your source code that's committed to version control.

Let's create a Navbar with an input box where we can securely enter the API key in the user interface. Place the following code inside pages/index.js:

import { useState } from "react";

export default function Home() {
  const [apiKey, setApiKey] = useState("");

  /* Add more logic here */

  return (
    <div className="flex flex-col h-screen">
      {/* Navbar */}
      <nav className="bg-white shadow w-full">
        <div className="px-4 h-14 flex justify-between items-center">
          <div className="text-xl font-bold">Jobot</div>
          <div>
            <input
              type="password"
              className="border rounded p-1"
              placeholder="Enter API key.."
              value={apiKey}
              onChange={(e) => setApiKey(e.target.value)}
            />
          </div>
        </div>
      </nav>

      {/* Add more UI here */}
    </div>
  );
}


TIP: Use Jobot's Code Explainer template to quickly understand any piece of code: https://jovian.com/jobot/code-explainer

This code is a functional React component that renders a navigation bar with a text input field to enter an API key. It uses Tailwind CSS utility classes for styling.

Here's a breakdown of the code (generated using Jobot) :

The code imports the useState hook from the react library.

The component is defined with the name Home and is exported as the default export of the module.

The useState hook is used to create a state variable apiKey and a function setApiKey to update it. The initial value of apiKey is an empty string.

The component returns a JSX element that contains a navigation bar with a text input field.

The navigation bar has a white background color and a shadow effect. It is fixed to the top of the viewport and spans the full width of the screen.

The navigation bar has a height of 14 pixels and contains two child elements.

The first child element is a div with a class of text-xl and font-bold. It displays the text "Jobot".

The second child element is a div that contains an input field.

The input field has a type attribute of "password", a className attribute of "border rounded p-1", a placeholder attribute with the text "Enter API key..", a value attribute that is bound to the apiKey state variable, and an onChange attribute that calls the setApiKey function whenever the input field is changed.

EXERCISES:

Learn more about React's useState hook here (10 mins): https://react.dev/learn/state-a-components-memory

Follow this tutorial to learn the basics of Tailwind CSS (12 min): https://www.youtube.com/watch?v=pfaSUYaSgRo

Chat Compeletion API
We can now use the chat completions OpenAI API endpoint to send a message to ChatGPT and get back the response:

The API endpoint is https://api.openai.com/v1/chat/completions

The HTTP method used to invoke the URL is POST

It expects a JSON request body in the following format:

{
  "model": "gpt-3.5-turbo",
  "messages": [{"role": "user", "content": "Hello!"}]
}
It expects the OpenAI API key to be passed in the header:
Authorization: Bearer OPENAI_API_KEY
It returns a response message in the following format:
{
  "id": "chatcmpl-123",
  "object": "chat.completion",
  "created": 1677652288,
  "choices": [{
    "index": 0,
    "message": {
      "role": "assistant",
      "content": "\n\nHello there, how may I assist you today?",
    },
    "finish_reason": "stop"
  }],
  "usage": {
    "prompt_tokens": 9,
    "completion_tokens": 12,
    "total_tokens": 21
  }
}


EXERCISES:

Learn more about OpenAI APIs here: https://platform.openai.com/docs/api-reference/introduction

Explore the documentation of the chat completions API here: https://platform.openai.com/docs/api-reference/chat/create

API Invocation with Fetch
Let's add a button below the navbar to invoke the chat completions API and show the response message below the button.

Add the following code above the comment /* Add more logic here */:

  const API_URL = "https://api.openai.com/v1/chat/completions";
  const [botMessage, setBotMessage] = useState("");
  const sendRequest = async () => {
    const response = await fetch(API_URL, {
      method: "POST",
      headers: {
        "Content-Type": "application/json",
        Authorization: `Bearer ${apiKey}`,
      },
      body: JSON.stringify({
        model: "gpt-3.5-turbo",
        messages: [{ role: "user", content: "Hello!" }],
      }),
    });

    const resJson = await response.json();
    console.log(resJson);

    setBotMessage(resJson.choices[0].message.content);
  };
  
  /* Add more logic here */
Here's a detailed explanation of the code:

const [botMessage, setBotMessage] = useState("") creates a state variable botMessage and a function setBotMessage to update the state. The initial value of botMessage is an empty string.

const sendRequest = async () => { ... } defines an asynchronous function sendRequest that makes a POST request to an API and sets the response as botMessage.

const response = await fetch(API_URL, { ... }) sends a POST request to the API_URL with the specified headers and body. The await keyword is used to wait for the response before moving on to the next line of code.

const resJson = await response.json() extracts the JSON data from the response using the json method.

setBotMessage(resJson.choices[0].message.content) updates the botMessage state with the first message from the response.

If apiKey is not defined or incorrect, the request might fail.

Add the following code above {/* Add more UI elements here */}:

  {/* Test Button */}
  <div className="p-4">
    <button
      onClick={sendRequest}
      className="w-40 bordered rounded bg-blue-500 hover:bg-blue-600 text-white p-2"
    >
      Send Request
    </button>
    <div className="mt-4 text-lg">{botMessage}</div>
  </div>

  {/* Add more UI elements here */}

Here's a detailed explanation of the code:

The code is written in JSX, which is a mix of JavaScript and HTML syntax.

The component is defined using the tag with a class name of "p-4".

Inside the tag, there is a tag with an "onClick" event listener that triggers the "sendRequest" function when clicked.

The button also has some classes for styling purposes (e.g., "bordered", "rounded", "bg-blue-500").

The text "Send Request" is the content of the button.

Below the button, there is another tag with a class name of "mt-4 text-lg".

Inside this tag, a variable called "botMessage" is displayed using curly braces {}.

The "botMessage" variable is most likely a string that is updated by the "sendRequest" function.

Once an appropriate API key is set in the header, clicking the button generates a response from the ChatGPT API.


EXERCISES:

Learn more about the JavaScript fetch function here: https://www.youtube.com/watch?v=cuEtnrL9-H0

Learn more about async and await in JavaScript here: https://www.youtube.com/watch?v=li7FzDHYZpc

Chat Interface Development
Let's review the given wireframe and problem statement:


PROBLEM: Build & deploy the chat interface shown in the above wireframe with the following features:

An input box where a user can enter a message and send it to Jobot

New messages from the user are sent to the OpenAI ChatGPT API

The response, along with the conversation history is shown above the input box

The user can provide their OpenAI API key in a secure input box in the page header

Message History & Chat Input
We can add the message history and chat input using the following code:


import { useState } from "react";
import Head from "next/head";

export default function Home() {
  const [apiKey, setApiKey] = useState("");
  const [userMessage, setUserMessage] = useState("");
  const [messages, setMessages] = useState([
    {
      role: "system",
      content:
        "You are Jobot, a helpful AI developed by Jovian and powered by state-of-the-art machine learning models.",
    },
  ]);

  const API_URL = "https://api.openai.com/v1/chat/completions";
  const sendRequest = async () => {
    const updatedMessages = [
      ...messages,
      {
        role: "user",
        content: userMessage,
      },
    ];

    setMessages(updatedMessages);
    setUserMessage("");

    try {
      const response = await fetch(API_URL, {
        method: "POST",
        headers: {
          "Content-Type": "application/json",
          Authorization: `Bearer ${apiKey}`,
        },
        body: JSON.stringify({
          model: "gpt-3.5-turbo",
          messages: updatedMessages,
        }),
      });

      const resJson = await response.json();
      console.log(resJson);

      const updatedMessages2 = [...updatedMessages, resJson.choices[0].message];
      setMessages(updatedMessages2);
    } catch (error) {
      console.error("error");
      window.alert("Error:" + error.message);
    }
  };

  return (
    <>
      <Head>
        <title>Jobot</title>
      </Head>
      <div className="flex flex-col h-screen">
        {/* Navbar */}
        <nav className="bg-white shadow w-full">
          <div className="px-4 h-14 flex justify-between items-center">
            <div className="text-xl font-bold">Jobot</div>
            <div>
              <input
                type="password"
                className="border rounded p-1"
                placeholder="Enter API key.."
                value={apiKey}
                onChange={(e) => setApiKey(e.target.value)}
              />
            </div>
          </div>
        </nav>

        {/* Message History */}
        <div className="flex-1 overflow-y-scroll">
          <div className="mx-auto w-full max-w-screen-md p-4 ">
            {messages
              .filter((msg) => msg.role !== "system")
              .map((msg, idx) => (
                <div key={idx} className="mt-3">
                  <div className="font-bold">
                    {msg.role === "user" ? "You" : "Jobot"}
                  </div>
                  <div className="text-lg">{msg.content}</div>
                </div>
              ))}
          </div>
        </div>

        {/* Message Input */}
        <div className="mx-auto w-full max-w-screen-md px-4 pt-0 pb-2 flex">
          <textarea
            className="border rounded-md text-lg p-2 flex-1"
            rows={1}
            placeholder="Ask me anything..."
            value={userMessage}
            onChange={(e) => setUserMessage(e.target.value)}
          />
          <button
            onClick={sendRequest}
            className="border rounded-md bg-blue-500 hover:bg-blue-600 text-white px-4 ml-2"
          >
            Send
          </button>
        </div>
      </div>
    </>
  );
}


EXERCISE: Generate explanations for various parts of the above code using Jobot's Code Explainer template: https://jovian.com/jobot

Adding Markdown Support
The chat completions API returns a response in the markdown format. We can render the markdown properly using the Tailwind CSS Typography plugin and the react-markdown library.

We can install the libraries as follows:
npm install @tailwindcss/typography react-markdown
Once installed, we need to add the plugin in tailwind.config.js:
module.exports = {
  theme: {
    // ...
  },
  plugins: [
    require('@tailwindcss/typography'),
    // ...
  ],
}

We can import the ReactMarkdown component in pages/index.js as follows:
import ReactMarkdown from `react-markdown`;
The message content in the message history can now be rendered by adding the prose-lg class and using the ReactMarkdown component:
<div className="prose-lg">
  <ReactMarkdown>{msg.content}</ReactMarkdown>
</div>
EXERCISES: Learn the basics of markdown in 20 minutes by following along with this tutorial: https://www.youtube.com/watch?v=HUBNt18RFbo

Cloud Deployment with Vercel
Vercel is a cloud platform that makes it easy to deploy websites and applications. It offers seamless integration with GitHub and other version control systems, allowing developers to deploy their projects directly from their repositories.


Follow these steps to deploy your website to Vercel:

Go to https://vercel.com and sign up for an account. You can use your GitHub account to sign up or create a new account using your email address.

Once you have signed up, you will be taken to the Vercel dashboard. From here, you can start a new project by clicking the "New Project" button.

Choose the repository you want to deploy. Vercel supports GitHub, GitLab, and Bitbucket repositories. Select the repository and the branch you want to deploy.

Select the project root folder (in this case, it is the src folder) and click "Deploy" to deploy the project. Make sure that the framework you're using is detected correctly.


Vercel will build your project and deploy it to its cloud platform. You can view your site by clicking the "Visit" button next to your project name. Example site: https://jovian-careers-site.vercel.app/

Whenever you push new changes to your repository, Vercel will automatically build and deploy your project to its cloud platform. This means that your site will always be up-to-date with your latest changes.

Bonus: Streaming the Message
Instead of waiting for the entire response to be generated, we can stream the message.

First, we need to install the eventsource-parser package:

npm install eventsource-parser
Next, we can import the createParser function:

import { createParser } from "eventsource-parser";

Then, we can update the sendRequest function as follows:

  const sendRequest = async () => {
    const updatedMessages = [
      ...messages,
      {
        role: "user",
        content: userMessage,
      },
    ];

    setMessages(updatedMessages);
    setUserMessage("");

    try {
      const response = await fetch(API_URL, {
        method: "POST",
        headers: {
          "Content-Type": "application/json",
          Authorization: `Bearer ${apiKey}`,
        },
        body: JSON.stringify({
          model: "gpt-3.5-turbo",
          messages: updatedMessages,
          stream: true,
        }),
      });

      const reader = response.body.getReader();

      let newMessage = "";
      const parser = createParser((event) => {
        if (event.type === "event") {
          const data = event.data;
          if (data === "[DONE]") {
            return;
          }
          const json = JSON.parse(event.data);
          const content = json.choices[0].delta.content;

          if (!content) {
            return;
          }

          newMessage += content;

          const updatedMessages2 = [
            ...updatedMessages,
            { role: "assistant", content: newMessage },
          ];

          setMessages(updatedMessages2);
        } else {
          return "";
        }
      });

      // eslint-disable-next-line
      while (true) {
        const { done, value } = await reader.read();
        if (done) break;
        const text = new TextDecoder().decode(value);
        parser.feed(text);
      }
    } catch (error) {
      console.error("error");
      window.alert("Error:" + error.message);
    }
  };


The message will now be streamed word by word and displayed on the screen.

Summary and Resources
The following topics were covered in this tutorial:

Understanding what it takes to build a AI-powered applications

Creating a chatbot UI similar to ChatGPT using React, NextJS & TailwindCSS

Connecting a chatbot UI to the OpenAI API & streaming messages

Deploying a chatbot UI to the cloud using GitHub and Vercel

The code for this tutorial can be found here:

Source code: https://github.com/jovianhq/jobot

Finished site: https://jobot.dev

Check out these resources to learn more about recent advances in artificial intelligence:

Sparks of AGI: https://arxiv.org/abs/2303.12712

Emergence: https://www.assemblyai.com/blog/emergent-abilities-of-large-language-models/

Check out these resources to learn the prerequisites for this tutorial:

HTML, CSS & JavaScript (30 mins) - https://www.youtube.com/watch?v=_GTMOmRrqkU

ReactJS (30 mins) - https://www.youtube.com/watch?v=hQAHSlTtcmY

NextJS (30 mins) - https://www.youtube.com/watch?v=OTuHnVvxTDs

Tailwind CSS (12 mins) - https://www.youtube.com/watch?v=pfaSUYaSgRo

CSS Flexbox (8 mins) - https://www.youtube.com/watch?v=phWxA89Dy94

Here's are some more optional, but useful tutorials:

Markdown: https://www.youtube.com/watch?v=HUBNt18RFbo

Visual Studio Code (8 mins) - https://www.youtube.com/watch?v=VqCgcpAypFQ

Git and GitHub (45 mins) - https://www.youtube.com/watch?v=tRZGeaHPoaw

NodeJS (16 mins) - https://www.youtube.com/watch?v=ENrzD9HAZK4

Fetch API (6 mins) - https://www.youtube.com/watch?v=cuEtnrL9-H0

Chrome Developer Tools Tutorial (50 mins) - https://www.youtube.com/watch?v=x4q86IjJFag

GitHub Codespaces (40 mins) - https://www.youtube.com/watch?v=D_5T6KMTRb8

JovianJobot - Learn with ChatGPT
Episode 1 - First Contact with Jobot | Jovian

## jovian-jobot - day - 2

