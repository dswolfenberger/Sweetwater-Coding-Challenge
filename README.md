# Sweetwater Product Review Challenge

In this project I recreated the product review experience that was provided. The Sweetwater prototype was a static figma file that I translated into a responsive, data-driven front-end experience.

The challenge could have been completed with HTML, CSS, and JavaScript alone. But instead, I chose to use **Vite, Vue, and SCSS** so that I could demonstrate how I approach reusable component development, structured styling, and interface decisions within a modern workflow. I chose to use VS Code as my IDE because it's my primary development environment that I'm familiar with, and I used Git to prepare the final project for the final review.

## Running the Project

### Requirements

Before downloading and running the project, ensure the following are installed on your machine:

- Git
- Node.js (includes npm)

### Setup

Open a terminal and navigate to the folder where you would like to save the project. Then run the following commands:

```bash
git clone https://github.com/dswolfenberger/Sweetwater-Coding-Challenge.git
cd Sweetwater-Coding-Challenge
npm install
npm run dev
```

The `npm install` command installs all required project dependencies, including Vue, Vite, and Sass.

Once the development server starts, open the local URL displayed in the terminal in your web browser (typically `http://localhost:5173/`).

To stop the development server, return to the terminal and press `Ctrl/Control + C`

## Tech Stack

- I used **Vite** for project setup and local development
- I used **Vue** to assist in building reusable, data-driven components
- I used **SCSS** for better styling and organization
- The 'reviews' **JSON** file includes the supplied review data
- **Git** was used for version control and to push the final project

## Project Structure

The full experience is divided into structured components so that each portion can be maintained and updated in single instances.

The file content structure:

- `ReviewForm` — this component displays the inputs and buttons for users to enter new reviews.
- `StarRating` — displays an existing star rating using filled and outlined stars.
- `RatingInput` — creates the star rating functionality displayed on the form.
- `ReviewList` — this component renders the existing user review data.
- `ReviewCard` — presents the user review data in individual review cards in an organized order.
- `ImageLightbox` — this feature allows users to expand submitted review images for a closer view of other users products.

## Development Approach

My goal while working on this project was to avoid overbuilding the exercise, but still show:

- how I interpreted the prototype and supporting data provided (like style guides, figma prototype decisions and UX adjustments)
- that I know how to determine when to divide an interface into reusable components
- that I can diagnose missing or unclear interaction state and assign proper accessible states to them without requiring designer clarity, based off of UX assumptions
- research details for best implementation practices and troubleshooting (such as reading devdocs.io, using AI tools, reading tech forums, or relying on predictive text to guide research when adding new features from scratch)
- That I can retain best accessibility, usability and SEO practices, making them a part of the development process from the start
- how I organize the files and code for projects I create without an existing tech stack, codebase and SDLC method.

## Important UX/UI Decisions

### Rating Input Component

The Figma prototype displayed user ratings (1-5) on the existing reviews, but it didn't include a way for users to add their rating when sending a new review.

I added a star rating radio selector input to the form, so the output review supports the same rating data shown on the review cards they see to the right of the form. The reason I chose radio inputs was to provide a familiar interaction and keep a polished, uninterrupted semantic flow.

### Alignment

Right when I looked at the prototype provided to me, I noticed general alignment issues around the project, not only with the equalness in the spacing between the review form, but also between the existing reviews, I established a spacing format and used that to ensure the project was aligned. Along with this I saw that the font was positioned lower within the buttons, which led me to believe it could have been an issue with padding, or even font alignment in the existing figma style guide structures. I used my UX thinking to formulate an assumption that this was not intentional and the buttons and fonts should be aligned both vertically and horizontally.

### Variable styling

I established from the start to keep a consistent style system, this helped avoid several inconsistencies in the provided prototype that I noticed.
A few of the alignment issues I saw were on the form, the button text and the headers were misaligned, so in my styling, I made sure to align the form and the inputs/buttons/titles properly.

### Brand Color Selection

The button colors in the prototype were different from Sweetwater's published brand guidance and current website components.

After studying the Sweetwater brand guide, I noticed that the color blue on the buttons didn't line up with the established color scheme. A quick check on existing buttons on the website showed that they were slightly different than the prototype color scheme. I chose to stay consistent with the established color guide and Sweetwater's brand in this challenge instead of assuming that the prototype provided to me was a new established guide.

In the instance I was working on a live environment with designers, I would choose to operate differently without assumption unless the new styling was predetermined and specified. In that case, I'd make sure I had an updated guide before continuing.

### Expandable Review Content

I noticed the truncated review text in the design was controlled with a **Read more** text link. I saw that the button wasn't styled appropriately to accessible standards. I decided to adjust the control with an underline so users can easily recognize that it's an interactive button. This was not based on an assumption, but rather on proper accessibility standards.

- [WebAIM: Link Text](https://webaim.org/techniques/hypertext/link_text)

### Select Files button

After I built the entire review experience from the prototype, I decided to spend dedicated time fixing the file selector so it matched what was provided. Originally, when I tried adding tags to adjust the styling, I wasn't able to change the native input field. I did some research using predictive text on google, scanned devdocs.io, stack overflow and vue/mdn documentation in those spaces. I continued facing the problem and was not making progress.

I used chatgpt to break through this problem and learn how to implement a fix for this in future development projects. I learned that I can keep the native input and its existing structure, but hide it so that I could use Vue templates to build a custom button. After I learned how to implement this into my existing code, without changing the established experience, it allowed me to match the styling to the prototype.

Documents, links and forums I read through:

- [Vue: Template Refs](https://vuejs.org/guide/essentials/template-refs.html)
- [MDN: File Input](https://developer.mozilla.org/en-US/docs/Web/HTML/Reference/Elements/input/file)
- [MDN: HTMLInputElement `files` Property](https://developer.mozilla.org/en-US/docs/Web/API/HTMLInputElement/files)
- [Stack Overflow: Bind File Input to a Button Using Vue.js](https://stackoverflow.com/questions/37535657/bind-file-input-to-a-button-using-vue-js)
- [Stack Overflow: Styling an Input Type File Button](https://stackoverflow.com/questions/572768/styling-an-input-type-file-button)

### Review Image Lightbox

In my project I decided to adjust the design so that review images could be opened in a lightbox. This allows users to see the product photos that others added in their reviews in a larger size without leaving the page. I used AI to develop this feature since it wasn't clearly included in the prototype provided, this allowed me to stay on track with the overall development. I included this adjustment to show my UX thinking outside of standard considerations.

### Text Area Resizing

The review text area was originally allowing user to expand vertically and horizontally. In my code I chose to restrict horizontal adjustments and give users control over the input height, keeping them from adjusting the form in a way that breaks the overall page layout.

## Accessibility Considerations

Throughout the development, I made sure accessibility was part of the process from the start, and throughout the components structure and interactions.

The project includes:

- semantic form controls
- properly associated labels and input IDs
- accessible names for interactive elements
- tested keyboard friendly page control
- visible interaction states
- proper page and heading structure
- commonly used radio inputs for the form rating selector
- image alternative text
- clear structure labeling

To confirm that my project was properly built, I ran the WAVE accessibility test again and found more issues, this time, the specific errors were contrast errors. After reading the error labels, determining the adjustments needed and adjusting the structure I was able to clear the errors.

I wasn't happy with the final experience and decided to restructure the component. I did some research and decided to use SVG Font Awesome icons. This helped clear the contrast problems and update to accessible standards. Through this process I improved the accessibility on the page, by adding fieldset and legend tags to properly label the rating group, I was also able to fix an orphaned label warning.

## Scope and Assumptions

Since the email specified that a header and footer navigation element wasn't needed for this project, those elements were excluded from the overall structure, and the form doesn't include the ability to submit new reviews.

Where inconsistencies in the prototype were presented, I made reasoned front-end focused assumptions and documented the adjustment around it, rather than assuming the prototype was the final say. This attention to detail made identifying the styles easier, in the event that adjustments to my assumption need to be made.

## Tools and Research

In the project I used a handful of resources during development:

- official Vite, Vue and SCSS documentation (as well as devdocs.io)
- browser developer tools (inspect element, debug, wave accessibility tool and Chrome VoiceOver)
- Sweetwater's online brand guidance and current website patterns
- Substack forum specific questions that have already been solved by the community
- and AI tools, like ChatGPT for focused setup guidance, troubleshooting, and implementation research.

## Future Improvements

With additional production requirements, I would consider adding:

- form validation and submission feedback
- API and database integration
- persistent uploaded images
- review sorting, filtering, and pagination

## References

- [Vue Component Basics](https://vuejs.org/guide/essentials/component-basics)
- [Semantic UI Rating Examples](https://semantic-ui.com/modules/rating.html)
