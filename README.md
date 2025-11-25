The Digital Garden



A minimalist, editorial-style personal website template designed for curating thoughts, code, and resources. Built with "Swiss Style" design principles and a Headless Firebase CMS.



Live Preview: \[Link to your site]



🏗 Architecture



The site is a "Dynamic Static" hybrid. Vercel/Netlify hosts the shell, and JavaScript fetches content from Firebase.



index.html - The Homepage. Fetches latest seeds (articles) from Firestore.



article.html - The Reading Template. Renders specific article content via URL ID.



admin.html - The CMS. A private dashboard to Write, Edit, and Delete entries.



about.html - The Author Profile.



404.html - Error page.



🚀 Setup Instructions



1\. Backend Setup (Firebase)

This site requires a Firebase project to store articles.

👉 Read FIREBASE\_SETUP.md for step-by-step configuration.



2\. Configuration

Once you have your Firebase keys, update the firebaseConfig object in index.html, article.html, and admin.html.



🎨 Design System



Typeface: Playfair Display (Headers), Inter (Body), JetBrains Mono (Data).



Colors: Ink (#1A1A1A) on Paper (#F4F4F0).



Texture: CSS-based noise overlay.



📝 License



Designed by \[Your Name]. Free to use and adapt.

