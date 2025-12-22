

## **Tech Brief: Integrating Dog CEO’s Dog API Into a Static Website**

**Objective:**  
Add an interactive widget to a static HTML/CSS website that displays a random dog breed and its image, leveraging the free and open [Dog CEO’s Dog API](https://dog.ceo/dog-api/).

**Key Points:**
- **API is free and requires no sign-up or authentication.**
- **Features:** List all breeds, fetch random breed images.
- Implementation uses only HTML, CSS, and Vanilla JavaScript.
- No backend or frameworks required, suitable for static hosting (e.g., Vercel).

---

## **Step-by-Step Implementation Plan**

### **Step 1: Understand the API**

- **List of all breeds:**  
  `GET https://dog.ceo/api/breeds/list/all`

- **Random image for a breed:**  
  `GET https://dog.ceo/api/breed/{breed}/images/random`  
  (replace `{breed}` with the breed name, e.g., `hound`)

---

### **Step 2: Add HTML Structure**

Create a container for the widget in your HTML file:

```html
<div id="dog-widget">
  <div id="breed-name">Loading...</div>
  <img id="dog-img" src="" alt="Dog image" style="display:none;">
  <button id="refresh-btn">Show Another Breed</button>
</div>
```

---

### **Step 3: Style the Widget (Optional)**

Add CSS to make the widget visually appealing:

```html
<style>
  #dog-widget {
    max-width: 350px;
    border: 1px solid #ccc;
    padding: 16px;
    text-align: center;
    border-radius: 8px;
    font-family: Arial, sans-serif;
    margin: 32px auto;
  }
  #dog-img {
    width: 100%;
    border-radius: 8px;
    margin-bottom: 12px;
  }
  #refresh-btn {
    margin-top: 10px;
    padding: 8px 16px;
    border: none;
    border-radius: 4px;
    background: #3399ff;
    color: white;
    cursor: pointer;
  }
  #breed-name {
    font-weight: bold;
    font-size: 1.2em;
    margin-bottom: 8px;
  }
</style>
```

---

### **Step 4: Fetch Breed Data and Images With JavaScript**

Add the following JavaScript to fetch and display random breeds and images:

```html
<script>
  let breedList = [];

  async function getBreeds() {
    const res = await fetch('https://dog.ceo/api/breeds/list/all');
    const data = await res.json();
    breedList = Object.keys(data.message);
  }

  async function showRandomBreed() {
    if (breedList.length === 0) await getBreeds();
    const breed = breedList[Math.floor(Math.random() * breedList.length)];
    document.getElementById('breed-name').innerText = breed.charAt(0).toUpperCase() + breed.slice(1);
    // get image
    const imgRes = await fetch(`https://dog.ceo/api/breed/${breed}/images/random`);
    const imgData = await imgRes.json();
    const img = document.getElementById('dog-img');
    img.src = imgData.message;
    img.style.display = '';
  }

  document.getElementById('refresh-btn').onclick = showRandomBreed;

  // Initial load
  showRandomBreed();
</script>
```

---

### **Step 5: Deploy**

1. **Copy and paste** the HTML, CSS, and JS into your main HTML file.
2. **Commit and push** your changes to your Git repository.
3. **Vercel will auto-deploy** your updated site.

---

## **Summary Table**

| Step | Action |
|------|--------|
| 1    | Learn the API endpoints |
| 2    | Add widget HTML |
| 3    | Style widget with CSS (optional) |
| 4    | Add JS to fetch and display data |
| 5    | Deploy updated site to Vercel |

---

**This approach requires no sign-up, no API key, and works instantly.**  
Let me know if you’d like the code as a complete copy-paste block or if you want to add features like breed search or display breed sub-types!