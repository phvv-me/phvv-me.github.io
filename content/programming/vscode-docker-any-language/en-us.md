---
title: How to start programming any language easy and fast
headline: How to setup vscode and docker to start programming in any language easy and fast
date: "2020-05-12"
description: a starter guide with vscode and docker for (almost) any language you want to start learning and developing - python, javascript, C#, rust, etc.
language: english
category: post
outdated: false
thumbnail:
  src: ../../images/two-woman-sitting-on-sofa-while-using-laptops.jpg
  alt: two women sitting on sofa while using laptops
  author:
    name: Christina @ wocintechchat.com
    href: wocintechchat.com
keywords:
  - tutorial
  - vscode
  - docker
  - python
  - javascript
  - node
  - c#
  - dotnetcore
---

<!-- ::absolute beginner : someone that does not know computers and programming, but wants to start learning it. -->
<!-- ::curious cat : someone who wants fast info and will skim the text for the necessary info. -->
<!-- 1. **bonus** - start a github project - before conclusion -->

<!-- ## Contents

- [Install Docker](#install-docker)
- [Install Visual Studio Code](#install-visual-studio-code)
- [Install the Remote Dev Extension](#install-remote-development-extension-pack)
- [Start with Python](#start-a-new-python-project)
- [Start with javascript](#start-a-new-javascript-project)
- [Start with C#](#start-a-new-c-net-core-project)
- [Conclusions](#conclusions)
- [References](#references)

--- -->

So you want to try a new programming language and don't know how to start, what to install nor which language to choose. Worry no more. This tutorial is designed to **enable you a fast and easy start** for any new project or computer idea you might have.

> **Note:** this is the basic tutorial for every other programming project in this website. Therefore, if you'd like to repeat my steps in another tutorial, this is the way to begin.

### Install Docker

#### Install Docker on Linux

1.  open the linux terminal (try <kbd>Ctrl</kbd> + <kbd>Alt</kbd> + <kbd>T</kbd> or look for it in the search bar)
2.  type the following commands:

    ```bash
    ❯ sudo apt-get update
    ❯ sudo apt-get install docker-ce docker-ce-cli containerd.io
    ```

3. for detailed instructions, refer to the [official docker engine installation guide][docker engine installation guide].

[docker engine installation guide]: https://docs.docker.com/engine/install/

#### Install Docker on MacOS

1. download Docker Desktop (Stable) for MacOS clicking [here][docker installer].
2. once it is downloaded, look for `Docker.dmg` file on Finder and click on it.
3. for detailed instructions, refer to the [official documentation][vscode docker remote containers docs].

#### Install Docker on Windows

1. download Docker Desktop (Stable) for Windows clicking [here][docker installer].
2. once it is downloaded, run the installer `Docker Desktop Installer.exe` file. You may need to restart your PC.
3. for detailed instructions, refer to the [official documentation][vscode docker remote containers docs].

[docker installer]: https://www.docker.com/products/docker-desktop
[vscode docker remote containers docs]: https://code.visualstudio.com/docs/remote/containers

### Install Visual Studio Code

#### Install Visual Studio Code on Linux

1. open the linux terminal (try <kbd>Ctrl</kbd> + <kbd>Alt</kbd> + <kbd>T</kbd> or look for it in the search bar)
2. install using snap

   ```bash
   ❯ sudo snap install --classic code # or code-insiders
   ```

3. if you saw errors, make sure you have `snapd` installed
   - some Linux distributions don't come with it pre-installed. If that's your case, [click here][snapd install] to go to the installation page and look for your distribution.
4. if you find any problems, look the [official Linux install guide][vscode linux install guide].

[snapd install]: https://snapcraft.io/docs/installing-snapd
[vscode linux install guide]: https://code.visualstudio.com/docs/setup/linux

#### Install Visual Studio Code on MacOS

1. download Visual Studio Code for macOS clicking [here][vscode macos installer].
2. open Finder and type `Visual Studio Code` on the search bar.
3. drag `Visual Studio Code.app` to the `Applications` folder, making it available in the macOS Launchpad.
4. add vscode to your Dock by right-clicking on the icon to bring up the context menu and choosing **Options**, **Keep in Dock**.
5. if you find any problems, look the [official MacOS install guide][vscode macos install guide].

[vscode macos installer]: https://code.visualstudio.com/docs?dv=osx
[vscode macos install guide]: https://code.visualstudio.com/docs/setup/mac

#### Install Visual Studio Code on Windows

1. download Visual Studio Code for Windows clicking [here][vscode windows installer].
2. once it is downloaded, run the installer (click on the `.exe` file).
3. vscode is by default installed at <i>`C:\users\{username}\AppData\Local\Programs\Microsoft vscode`</i>
4. if you find any problems, look the [official Windows install guide][vscode windows install guide].

[vscode windows installer]: https://code.visualstudio.com/docs?dv=win
[vscode windows install guide]: https://code.visualstudio.com/docs/setup/windows

### Install Remote Development extension pack

With Docker and Visual Studio Code installed, we just need the **Remote Development vscode extension**. Click on the link below to go to the download page.

<!-- TODO: componentize -->
[link to remote development extension](https://marketplace.visualstudio.com/items?itemName=ms-vscode-remote.remote-containers)

### Start a new python project

1. click on the new symbol in the lower left corner. A dropdown list of options will appear.
2. select **Remote-Containers: Try a Sample...** from the command list. A list of the available languages will be shown.
3. choose **Python**. The screen will blink and start downloading the images to start your project.
4. this step may take from **5 to 15 minutes**. Wait for it to finish.
5. after the download is over, on vscode, an **workspace** will be created with the project files.
6. if you have any doubts, **check the video below** to see each step exactly.

`video: title: "create vscode python project": ./videos/python.mov`

#### Explaining the `vscode-remote-try-python` files

Below you'll find some explanations about all the project files. If you're just beginning or new to python, focus on the `.py` file and don't worry much about the others. Any important files ones will be highlighted or emphasized.

<FileTreeView placeholder="vscode project explorer. Click an icon on the left to see some explanations.">
  <Folder name=".devcontainer">
    vscode Remote Containers extension specific folder. It uses <code>devcontainer.json</code> and an optional
    <code>Dockerfile</code> or <code>docker-compose.yml</code> to create the development containers.
    <File name="devcontainer.json">
      After the docker image is assembled by the Dockerfile, a container is created and started using the settings in
      <code>devcontainer.json</code>. It can also modify some configurations of the Dockerfile, as for this project, the Python
      version is redefined to 3.7 with the VARIANT arg. This file also contains settings
      for the Visual Studio Code environment.
    </File>
    <File name="Dockerfile">
      This file is referenced at `devcontainer.json` to 
      <a href="https://docs.docker.com/engine/reference/builder/">assemble a docker image</a>.
      Then, a container is created and started using some of the settings in `devcontainer.json`.
    </File>
  </Folder>
  <Folder name=".vscode">
    vscode settings folder. It is used for project specific configurations.
    <File name="launch.json">
      This file has running and debugging configuration information. It is very useful for automation and storing some
      environment variables for development purposes.
    </File>
  </Folder>
  <Folder name="static">
    A folder for all the static files: files that never change and can be send as they are. In web projects, they
    usually have images, icons, `HTML`, `CSS` and `javascript` files.
    <File name="index.html">
      A simple `.html` file with the landing page that will be sent by the server created by `app.py`.
    </File>
  </Folder>
  <File name=".gitattributes">
    A git related file. It sets some attributes to the files being committed. In our case, it normalizes line endings
    for Windows OS specific files (.cmd, .bat).
  </File>
  <File name=".gitignore">
    A git related file. It is a list of all files and folder that the git repo should ignore.
  </File>
  <File name="app.py">The python file. It starts a flask server that sends the `index.html` file.</File>
  <File name="LICENSE">
    An open source license file. It specifies how you, me and other developers can use this project. In our case, we
    have a <a href="https://choosealicense.com/licenses/mit/">MIT License</a>.
  </File>
  <File name="README.md">
    This is a very common file among programming projects. It is a markdown file with instructions on how to start the
    project and with some ideas and things to try.
  </File>
  <File name="requirements.txt">
    This is a very common file among python projects. It is a text file that disposes all the dependencies that need to
    be installed with `pip` before the project can run.
  </File>
</FileTreeView>

#### How to run your `vscode-remote-try-python` project

1. Open the vscode terminal window. Notice it is already connected to the docker container.
2. In the terminal, type the command below to run the app.
   ```bash
   python -m flask run --port 9000 --no-debugger --no-reload
   ```
3. Open your browser (Safari, Edge, Firefox, Chrome, Opera, ...) and go to [http://localhost:9000](http://localhost:9000) to see the running app.

### Start a new javascript project

1. Click on the new symbol in the lower left corner. A dropdown list of options will appear.
2. Select **Remote-Containers: Try a Sample...** from the command list. A list of the available languages will be shown.
3. Choose **Node**. The screen will blink and start downloading the images to start your project.
4. This step may take from **5 to 15 minutes**. Wait for it to finish.
5. After the download is over, on vscode, an **workspace** will be created with the project files.
6. If you have any doubts, **check the video below** to see each step exactly.

`video: title: "create vscode node project": ./videos/node.mov`

#### Explaining the `vscode-remote-try-node` files

Below you'll find some explanations about all the project files. If you're just beginning or new to javascript, focus on the `.js` file and don't worry much about the others. Any important files ones will be highlighted or emphasized.

<FileTreeView placeholder="vscode project explorer. Click an icon on the left to see some explanations.">
  <Folder name=".devcontainer">
    vscode Remote Containers extension specific folder. It uses <code>devcontainer.json</code> and an optional
    <code>Dockerfile</code> or <code>docker-compose.yml</code> to create the development containers.
    <File name="devcontainer.json">
      After the docker image is assembled by the Dockerfile, a container is created and started using the settings in
      <code>devcontainer.json</code>. It can also modify some configurations of the Dockerfile. This file also contains settings
      for the Visual Studio Code environment.
    </File>
    <File name="Dockerfile">
      This file is referenced at <code>devcontainer.json</code> to 
      <a href="https://docs.docker.com/engine/reference/builder/">assemble a docker image</a>. 
      Then a container is created and started using some of the settings in <code>devcontainer.json</code>.
    </File>
  </Folder>
  <Folder name=".vscode">
    vscode settings folder. Used for project specific configurations.
    <File name="launch.json">
      This file has running and debugging configuration information. It is very useful for automation and storing some
      environment variables for development purposes.
    </File>
  </Folder>
  <Folder name="node_modules" closed gray>
    A folder for all the installed project dependencies. All dependencies are listed on the <code>package.json</code>.
  </Folder>
  <File name=".eslintrc.json">
    The eslint settings file. It configures the javascript linter eslint for the project. A linter is responsible for
    finding and fixing some non technical issues and enforce good practices in the code. It does not format the code
    however! This is the job of tools like Prettier.
  </File>
  <File name=".gitattributes">
    A git related file. It sets some attributes to the files being committed. In our case, it normalizes line endings
    for Windows OS specific files (.cmd, .bat).
  </File>
  <File name=".gitignore">
    A git related file. It is a list of all files and folder that the git repo should ignore.
  </File>
  <File name="LICENSE">
    An open source license file. It specifies how you, me and other developers can use this project. In our case, we
    have a <a href="https://choosealicense.com/licenses/mit/">MIT License</a>.
  </File>
  <File name="package.json">
    This is very common file among javascript projects. It contains several settings on how to start running the project
    and the dependencies that need to be installed.
  </File>
  <File name="README.md">
    This is a very common file among programming projects. It is a markdown file with instructions on how to start the
    project and with some ideas and things to try.
  </File>
  <File name="server.js">
    The javascript file. It starts an express server that sends a 'Hello World' message and prints on the console a link
    to it.
  </File>
  <File name="yarn.lock">
    A yarn related file. Yarn is one of the available javascript package managers and this file tells yarn how to find
    all the necessary dependency packages easier and faster.
  </File>
</FileTreeView>

#### How to run your `vscode-remote-try-node` project

1. Press <kbd>F5</kbd> to launch the app in the container. The file `launch.json` has configured vscode how to start it. It will be started in debugging mode.
2. Open your browser (Safari, Edge, Firefox, Chrome, Opera, ...) and go to [http://localhost:9000](http://localhost:9000) to see the running app.

### Start a new C# .NET Core project

1. Click on the new symbol in the lower left corner. A dropdown list of options will appear.
2. Select **Remote-Containers: Try a Sample...** from the command list. A list of the available languages will be shown.
3. Choose **.NET Core**. The screen will blink and start downloading the images to start your project.
4. This step may take from **5 to 15 minutes**. Wait for it to finish.
5. After the download is over, on vscode, an **workspace** will be created with the project files.
6. If you have any doubts, **check the video below** to see each step exactly.

`video: title: "create vscode dotnetcore project": ./videos/dotnetcore.mov`

#### Explaining the `vscode-remote-try-dotnetcore` files

Below you'll find some explanations about all the project files. If you're just beginning or new to C#, focus on the `.cs` file and don't worry much about the others. Any important files will be highlighted or emphasized.

<FileTreeView placeholder="vscode project explorer. Click an icon on the left to see some explanations.">
  <Folder name=".devcontainer">
    vscode Remote Containers extension specific folder. It uses <code>devcontainer.json</code> and an optional
    <code>Dockerfile</code> or <code>docker-compose.yml</code> to create the development containers.
    <File name="devcontainer.json">
      After the docker image is assembled by the Dockerfile, a container is created and started using the settings in
      <code>devcontainer.json</code>. It can also modify some configurations of the Dockerfile. This file also contains settings
      for the Visual Studio Code environment.
    </File>
    <File name="Dockerfile">
      This file is referenced at <code>devcontainer.json</code> to 
      <a href="https://docs.docker.com/engine/reference/builder/">assemble a docker image</a>. 
      Then a container is created and started using some of the settings in <code>devcontainer.json</code>.
    </File>
  </Folder>
  <Folder name=".vscode">
    vscode settings folder. Used for project specific configurations.
    <File name="launch.json">
      This file has running and debugging configuration information. It is very useful for automation and storing some
      environment variables for development purposes.
    </File>
    <File name="tasks.json">
      This file <a href="https://code.visualstudio.com/docs/editor/tasks">define some scripts that can be used by vscode</a> in <code>launch.json</code> for instance. In our case, the tasks <code>build</code>, <code>publish</code> and <code>watch</code> are defined in this file. The <code>build</code> task is then referenced in <code>launch.json</code>.
    </File>
  </Folder>
  <Folder name="bin" closed gray>
    This folder can be ignored. The bin folder holds binary files: the executable, compiled code for the application. 
  </Folder>
  <Folder name="obj" closed gray>
    This folder can be ignored. This folder holds intermediate files, which will be combined to produce the final executable. The compiler generates one of these files for each source file, and they are placed into the obj folder.
  </Folder>
  <File name=".gitignore">
    A git related file. It is a list of all files and folder that the git repo should ignore.
  </File>
  <File name="appsettings.Development.json">
    This file overwrites the values defined at <code>appsettings.json</code> for the Development build.
  </File>
  <File name="appsettings.HttpsDevelopment.json">
    This file overwrites the values defined at <code>appsettings.json</code> and <code>appsettings.Development.json</code> for the Https channel in Development build.
  </File>
  <File name="appsettings.json">
    This file defines variables and configurations to be used by the application. It can be split into other versions for specific groups of variables and environments, such as Development, HttpsDevelopment, Production, etc.
  </File>
  <File name="aspnetapp.csproj">
    This file is mandatory for C# projects. It is a MSBuild project file specific for C# projects. It can specify dependencies and a few extra configurations for the project. In our case, it specifies the .NET Core version and the secret storage id.
  </File>
  <File name="LICENSE">
    An open source license file. It specifies how you, me and other developers can use this project. In our case, we
    have a <a href="https://choosealicense.com/licenses/mit/">MIT License</a>.
  </File>
  <File name="program.cs">
    The C# file. It starts an ASP.NET Core server that sends a 'Hello World' message.
  </File>
  <File name="README.md">
    This is a very common file among programming projects. It is a markdown file with instructions on how to start the
    project and with some ideas and things to try.
  </File>
</FileTreeView>

#### How to run your `vscode-remote-try-dotnetcore` project

1. Press <kbd>F5</kbd> to launch the app in the container. The file `launch.json` has configured vscode how to start it. It will be started in debugging mode.
2. Open your browser (Safari, Edge, Firefox, Chrome, Opera, ...) and go to [http://localhost:5000](http://localhost:5000) to see the running app.

## Conclusions

In this tutorial, we learned how to start a new project from a variety of languages easily. For that, we installed the Docker container platform, the Visual Studio Code Editor and the Remote Development vscode extension. These tools are useful if you are starting a new project or want to start learning a new programming language. A few remarks and observations are listed below about this approach.

1. **Simplicity:**
   - simple installation previous to coding.
   - we can **try another language in vscode** just by repeating the same steps.
   - we didn't face any of the _"headaches"_ that beginners suffer when trying a new language.
2. **Security:**
   - Docker creates a **safety layer**. Therefore, you can play and try anything you want without worrying about damaging anything in your computer.
3. **Containerization:**
   - Docker: It will **always** work in your machine!
   - No virtual environments. The Docker container works as one.
   - We don't need to download vscode extensions for each language. vscode server installs all the necessary extensions automatically based on the language you choose.
4. **Disadvantages:**
   - **Startup:** the first time you start your application will be slow, as vscode has to download and build the Docker images. _P.S.: I know I wrote **fast** in the title, but I am considering the amount of time the average person would have troubleshooting everything that could go wrong with installing each language, especially beginners._
   - **Memory:** Docker containers add some overhead to MacOS and Windows applications, but usually you won't notice that. Look at Docker Desktop for more info about your containers.
   - **Absolute Beginners:** If you are just starting to learn how to program, some of the steps could come as difficult, especially the Docker part. As I said before, try not to worry too much about it: you'll see that a lot of things in programming mix different technologies and I believe it's important to get used to it from the start.

**Happy Coding! 🧑🏻‍💻**

## Further Reading

Microsoft has all the process of [Setting the Container Development in vscode](https://code.visualstudio.com/remote-tutorials/containers/how-it-works) and [Developing inside a Container](https://code.visualstudio.com/docs/remote/containers) well documented. It's definitely worth checking it out.
