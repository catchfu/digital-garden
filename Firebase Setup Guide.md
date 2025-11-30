Firebase Configuration Guide



This project uses Firebase for Authentication and Database.



1\. Create Project



Go to Firebase Console.



Create a new project (e.g., digital-garden).



Disable Google Analytics.



2\. Enable Authentication



Go to Build > Authentication.



Click Get Started.



Enable Email/Password.



Create your Admin Account: Go to the "Users" tab and "Add user" (this will be your login for admin.html).



3\. Enable Firestore Database



Go to Build > Firestore Database.



Create Database (Production Mode).



Select a location near you.



4\. Security Rules (CRITICAL)



Go to the Rules tab in Firestore and paste the following. This configuration allows public access to the blog but restricts the Admin OS to you and people you explicitly share with.



rules\_version = '2';

service cloud.firestore {

&nbsp; match /databases/{database}/documents {

&nbsp;   

&nbsp;   // 1. PUBLIC BLOG (Read-only for public)

&nbsp;   match /artifacts/{appId}/public/data/posts/{document=\*\*} {

&nbsp;     allow read: if true; // Public can read all (code filters drafts)

&nbsp;     allow write: if request.auth != null; // Only logged in users can write

&nbsp;   }



&nbsp;   // 2. USER DATA (Strict Ownership \& Sharing)

&nbsp;   // Applies to 'todos' and 'events'

&nbsp;   match /artifacts/{appId}/users/{userId}/{allPaths=\*\*} {

&nbsp;     allow read, write: if request.auth != null \&\& (

&nbsp;       request.auth.uid == userId || 

&nbsp;       resource.data.sharedWith.hasAny(\[request.auth.token.email])

&nbsp;     );

&nbsp;   }

&nbsp; }

}





5\. Get API Keys



Click the Gear Icon > Project Settings.



Scroll to "Your apps" and create a Web App.



Copy the firebaseConfig object.



Paste it into the top of index.html, admin.html, and article.html.

