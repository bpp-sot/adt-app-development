# Setting Up Your Development Environment

## Overview

These instructions will guide you through creating your own development repository using GitHub and setting up a React application using Codespaces. The process is divided into three main sections: creating your repository, launching your development environment, and initialising your React application.

---

## Section 1: Creating Your Repository

**What you're doing:** You'll be creating your own copy of the template repository where you can work on your project independently.

1. **Access GitHub**
    
    - Log in to GitHub, or sign up using your @my.bpp.com email address if you don't yet have an account
2. **Navigate to the template repository**
    
    - Go to https://github.com/bpp-sot/adt-app-development
3. **Create your repository from the template**
    
    - Click the green **'Use this template'** button (located near the top right of the page)
    - Select **'Create a new repository'** from the dropdown menu
    
    _Note: Using a template creates a fresh copy of the repository rather than forking it, giving you a clean starting point for your own work._
    
4. **Configure your repository**
    
    - Edit the repository name in the text field (alternatively, you can click on the auto-generated suggested name that appears below)
    - Change the visibility setting to **'Public'**
    
    _Note: Making your repository public allows tutors to view your work and helps build your professional portfolio._
    
5. **Finalise creation**
    
    - Click the green **'Create repository'** button
    - Wait a moment whilst GitHub creates your new repository

---

## Section 2: Launching Your Development Environment

**What you're doing:** You'll be setting up a cloud-based development environment (Codespace) that provides you with a fully configured workspace without needing to install anything on your local machine.

6. **Create a Codespace**
    
    - Once your repository has been created, click the green **'<> Code'** button
    - Select the **'Codespaces'** tab from the menu
    - Click the green **'Create codespace on main'** button
    
    _Note: This process may take 1-2 minutes as GitHub sets up your virtual development environment. A new browser tab will open with Visual Studio Code (VSCode)._
    
7. **Open a terminal**
    
    - At the top of the VSCode interface, locate the search bar (this is within the application, not your browser's search bar)
    - Click on the search bar and a dropdown menu will appear
    - Click **'Show and run commands'**
    - In the command palette, search for and click **'Terminal: Create New Terminal'**
    
    _Note: The terminal is where you'll type commands to control your development environment. A terminal pane will open at the bottom of the page._
    

---

## Section 3: Initialising Your React Application

**What you're doing:** You'll be using Vite (a modern build tool) to create a React application structure with all the necessary files and dependencies.

8. **Create the React application**
    
    - In the terminal pane at the bottom of the screen, type the following command exactly as shown:
        
        ```
        npm create vite@latest . -- --template react
        ```
        
    - Press **Enter**
    
    _Note: This command tells npm (Node Package Manager) to create a new Vite project using the React template in the current directory._
    
9. **Respond to the setup prompts**
    
    You'll be asked several questions. Respond as follows:
    
    - **'Current directory is not empty. Please choose how to proceed'**
        
        - Choose **'Ignore files and continue'** and press **Enter**
        
        _This allows Vite to set up the project alongside the existing GitHub files._
        
    - **'Use rolldown-vite (Experimental)?'**
        
        - Choose **'No'** and press **Enter**
        
        _Rolldown is an experimental feature that we don't need for this project._
        
    - **'Install with npm and start now?'**
        
        - Choose **'Yes'** and press **Enter**
        
        _This automatically installs all required packages and starts your development server._
        
10. **Open your running application**
    
    - Once the installation completes, look for a link in the terminal that reads `http://localhost:5173`
    - Hold the **Ctrl** key (or **Cmd** on Mac) and click the link
    
    _Note: This opens your application in a new browser tab. You're now viewing your React application running in development mode! Any changes you make to your code will automatically refresh in this preview._
    

---

## Troubleshooting Tips

- If the terminal doesn't appear, try using the keyboard shortcut **Ctrl + `** (backtick) to toggle it
- If you encounter permission errors, ensure you're logged into GitHub with your @my.bpp.com account
- If the preview doesn't load, check the terminal for error messages
- You can stop the development server at any time by pressing **Ctrl + C** in the terminal

---

**Next Steps:** You're now ready to begin developing your React application! Any changes you make to files in the `src` folder will automatically appear in your preview window.
