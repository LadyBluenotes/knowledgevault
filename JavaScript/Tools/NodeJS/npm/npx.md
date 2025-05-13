- Powerful command
- If you do not want to install npm, you can install npx as a _standalone package_
- Lets you run npm registry without needing to install the package itself
- Takes care of:

  1. Downloading the package on-the-fly
  2. Running the desired command
  3. Cleaning up the temporary installation

- Useful for:
  - Trying out new tools
  - Running one-time commands
  - Using packages in a shared environment where global installations are undesirable
  - Keeping project dependencies lean
  - Avoiding version conflicts
