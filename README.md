# Source Mapping Works in VS Code, but not nvim/nvim-dap

This is a minimal example of the problems I'm having trying to debug a
containerized remix.run application with nvim/nvim-dap. Debugging this project
works fine on VS Code, but does not work for nvim/nvim-dap.

## Steps to Reproduce

1. Clone this repository
2. Install and build to get the output files "locally." In a typical project
   where you mount your whole source tree into the container for development
   and a live-reload server pumps new build files into your source tree, this
   wouldn't be necessary, but you won't have the output files on your machine
   in this setup if you skip this step.
   ```
   npm install && npm run build
   ```
3. Startup docker-compose, which will run the debug script inside a container
   and expose port 9229
   ```
   docker-compose up
   ```
4. Try attaching a debugger and debugging in VS Code and neovim/nvim-dap

You will notice that in VS Code, the debugger is able to read the source map,
will step through `main.ts` instead of the generated `main.js`, and breakpoints
you set in `main.ts` will work.

In neovim/nvim-dap with the vscode-node2-debug adapter, the debugger will
attach, but it will step through the generated `main.js`. Breakpoints set in
`main.ts` will not work and an error is emitted, `"Breakpoint ignored because
generated code not found (source map problem?)."`
