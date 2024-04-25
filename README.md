# Svelcordot

Svelcordot is a template repository with a simple setup for integrating your Discord Activity with SvelteKit. This project utilizes a Godot WebGL build to display your Discord activity seamlessly. As an example, a pong game built with Godot is included in this template.

## Features

-   Easy integration of Discord Activity with SvelteKit
-   Godot WebGL build for interactive content
-   Minimal setup and configuration required
-   Includes a sample pong game built with Godot

## Prerequisites

-   Godot Engine
-   Node.js
-   npm (Node Package Manager)
-   GitHub Desktop (optional, but recommended for easier repository management)

## Getting Started

To get started with Svelcordot, follow these steps:

1. Click the "Use this template" button on the GitHub repository page to create a new repository based on this template.

2. Clone your newly created repository using GitHub Desktop or the command line:

    ```
    git clone https://github.com/yourusername/your-repo-name.git
    ```

3. Navigate to the project directory:

    ```
    cd your-repo-name
    ```

4. Install the dependencies:

    ```
    npm install
    ```

5. Create a `.env` file in the root directory of the project and add your Discord application's `CLIENT_ID` and `CLIENT_SECRET` for server-side authentication:
    ```
    CLIENT_ID=your_client_id
    CLIENT_SECRET=your_client_secret
    ```

## Setting Up Godot WebGL

1. Open your Godot project and select the **WebGL** export template.

2. Configure the export settings for your Godot project.
    - Note if using Godot 4, you must disable Thread Support in the export settings. (currently only available in the Godot 4.3(dev5))

3. Export your Godot project as a WebGL build and locate the generated files.

## Configuration

1. Open your project's `lib` folder and set up your configuration file (`config.ts`) with the necessary details.

2. Copy the exported Godot WebGL files you generated earlier and paste them into this project's `static` folder.

## Usage

1. Run the development server to test the project:

    ```
    npm run dev
    ```

2. Open your browser and visit `https://localhost:5173` to see your Discord Activity in action.

3. When you're ready to deploy, build the project:

    ```
    npm run build
    ```

    Note: In the `svelte.config.js` file, make sure to replace `adapter: adapter()` with an adapter of your choice, depending on your deployment platform. SvelteKit offers various official and community adapters for different platforms.

    For example, if you want to use the `@sveltejs/adapter-node` adapter for deploying to platforms that support Node.js (e.g., AWS, Azure, Heroku), you would modify your `svelte.config.js` file like this:

    ```js
    // svelte.config.js
    import { vitePreprocess } from "@sveltejs/kit/vite";
    import adapter from "@sveltejs/adapter-node";

    const config = {
        preprocess: vitePreprocess(),
        kit: {
            adapter: adapter(),
        },
    };

    export default config;
    ```

    Make sure to install the corresponding adapter package. For example, if using `@sveltejs/adapter-node`:

    ```
    npm install @sveltejs/adapter-node
    ```

    Don't forget to remove `@sveltejs/adapter-auto` from `package.json` if you're using a specific adapter!

    You can explore other official and community adapters in the SvelteKit documentation to find the one that suits your deployment needs.

4. Deploy the built files to your chosen platform if you want to share your Discord Activity with others (Discord Proxy).

5. Enjoy your Discord Activity powered by SvelteKit and Godot WebGL!

Remember to choose an adapter that matches your deployment platform and follow the specific deployment instructions for that platform.

## Example: Pong Game

This template includes a sample pong game built with Godot to demonstrate how to integrate a Godot WebGL build with SvelteKit. The game files are in the static folder.  

Feel free to replace the example game with your Godot WebGL build to showcase your Discord Activity.  

## Contributing

Contributions are welcome! If you find any bugs or have suggestions for improvement, please open an issue or submit a pull request.

## License

This project is licensed under the [MIT License](LICENSE).

---

In the words of Todd Howard, it just works.
