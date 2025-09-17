# ramp-frontend-code-challenge
Created with CodeSandbox
Ramp CTF Challenge Solution
A React-based solution for the Ramp Frontend Developer Challenge featuring DOM parsing and typewriter animation effects.
Live Demo
You can access the live demo [here](https://wvfvk5.csb.app/).
Challenge Overview
This project solves a Capture The Flag (CTF) challenge that involves:

Extracting a hidden URL from DOM elements using a specific pattern
Creating a React application with a typewriter effect
Fetching and displaying the flag character by character

Solution Details
Step 1: URL Extraction
Used JavaScript to parse the DOM and extract characters from elements matching this pattern:
html<section data-id="92*">
  <article data-class="*45">
    <div data-tag="*78*">
      <b class="ref" value="VALID_CHARACTER"></b>
    </div>
  </article>
</section>
Hidden URL Found: https://wgg522pwivhvi5gqsn675gth3q0otdja.lambda-url.us-east-1.on.aws/636865
Flag: cheerly
Step 2: React Application
Created a React app that:

Fetches the flag from the hidden URL
Displays "Loading..." during fetch
Implements typewriter effect (500ms delay between characters)
Renders each character as a list item
Uses only React APIs (no external libraries)

Technical Implementation
URL Extraction Script
javascriptfunction extractHiddenURL() {
  const sections = document.querySelectorAll('section[data-id^="92"]');
  const characters = [];
  
  sections.forEach(section => {
    const article = section.querySelector('article[data-class*="45"]');
    if (article) {
      const div = article.querySelector('div[data-tag*="78"]');
      if (div) {
        const b = div.querySelector('b.ref[value]');
        if (b) {
          const char = b.getAttribute('value');
          if (char) {
            characters.push(char);
          }
        }
      }
    }
  });
  
  return characters.join('');
}
React Typewriter Effect
javascriptuseEffect(() => {
  if (!isLoading && flag && currentIndex < flag.length) {
    const timer = setTimeout(() => {
      setDisplayedChars(prev => [...prev, flag[currentIndex]]);
      setCurrentIndex(prev => prev + 1);
    }, 500);
    
    return () => clearTimeout(timer);
  }
}, [flag, currentIndex, isLoading]);
Running Locally
bash# Install dependencies
npm install

# Start development server
npm start

# Build for production
npm run build
Requirements Met

✅ Extract hidden URL from specific DOM pattern
✅ HTTP request using browser APIs (fetch)
✅ Loading state display
✅ Typewriter effect with 500ms delay
✅ Characters rendered as list items
✅ React APIs only (no CSS animations or external libraries)
✅ Animation triggers after loading
✅ Animation runs only once

Final Submission
cheerly - https://wvfvk5.csb.app/
