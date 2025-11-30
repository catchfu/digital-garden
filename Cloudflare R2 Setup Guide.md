Cloudflare R2 Setup (For Large Attachments)

To avoid Firebase Storage costs, this project uses a Cloudflare Worker to upload large files (images/videos > 500KB) to an R2 bucket.

Cost: Free tier includes 10GB storage and millions of requests.

1. Create R2 Bucket

Log in to Cloudflare Dashboard.

Go to R2 > Create Bucket.

Name it garden-assets.

Enable Public Access:

Go to Settings tab.

Under "Public Access", click "Allow Access" (or connect a custom domain).

Copy the Public R2.dev URL (e.g., https://pub-xyz.r2.dev).

2. Create the Worker (The Bridge)

Go to Workers & Pages > Create Worker.

Name it garden-uploader.

Click Deploy, then Edit Code.

Paste the following code into worker.js:

export default {
  async fetch(request, env) {
    const corsHeaders = {
      "Access-Control-Allow-Origin": "*",
      "Access-Control-Allow-Methods": "PUT, DELETE, OPTIONS",
      "Access-Control-Allow-Headers": "Content-Type, X-Custom-Auth",
    };

    if (request.method === "OPTIONS") {
      return new Response(null, { headers: corsHeaders });
    }

    const auth = request.headers.get("X-Custom-Auth");
    if (auth !== env.UPLOAD_SECRET) {
      return new Response("Unauthorized", { status: 403, headers: corsHeaders });
    }

    const url = new URL(request.url);
    const key = url.pathname.slice(1);

    // PUT (Upload)
    if (request.method === "PUT") {
      await env.BUCKET.put(key, request.body);
      return new Response(`${env.PUBLIC_URL}/${key}`, { headers: corsHeaders });
    }

    // DELETE (Remove)
    if (request.method === "DELETE") {
      await env.BUCKET.delete(key);
      return new Response("Deleted", { status: 200, headers: corsHeaders });
    }

    return new Response("Method not allowed", { status: 405, headers: corsHeaders });
  }
};


3. Connect Worker to Bucket

Go to the Worker's Settings > Variables.

R2 Bucket Binding:

Variable name: BUCKET

Select your garden-assets bucket.

Environment Variables:

UPLOAD_SECRET: Create a password (e.g., MySecretPassword123).

PUBLIC_URL: Paste your R2 Public URL from Step 1 (NO trailing slash).

Click Deploy.

4. Connect to Admin Panel

Copy your Worker URL (e.g., https://garden-uploader.user.workers.dev).

Open admin.html.

Update the config section:

const cloudflareWorkerUrl = "[https://your-worker-url.workers.dev](https://your-worker-url.workers.dev)";
const cloudflareSecret = "MySecretPassword123";
