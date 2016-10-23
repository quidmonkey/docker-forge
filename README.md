<p align="center">
  <a href="https://github.com/quidmonkey/forge">
    <img height="200" width="176" src="https://www.dropbox.com/s/o14iy9b7ng5y5jy/Forge-logo-16color-439x500.png?dl=1">
  </a>
  <p align="center">The task runner for scalable local development</p>
</p>

## What is Docker-Forge?

Docker-Forge offers up two containerization solutions for working with [forge](https://github.com/quidmonkey/forge):

1. executable - dynamically execute forge commands within a container easily with the following alias:
```
alias forge=executable_forge
executable_forge() {
    docker run -it --rm \
        -v $(pwd):/data \
        -v $HOME/.ssh:/root/.ssh \
        --name forge \
        quidmonkey/forge-executable:latest "$@"
}
```

2. interactive - offers up a interactive container for working for forge - forge is installed globally:
```
alias run_forge=interactive_forge
interactive_forge() {
    docker run -it \
        -v $(pwd):/data \
        -v $HOME/.ssh:/root/.ssh \
        --name forge \
        quidmonkey/forge-interactive:latest /bin/bash
}
```

Both of these are to be used for local development and are designed to have a corresponding forge project mounted. The thinking behind this is to avoid having to manage project dependencies. By mounting any locally installed gem, pip, or npm dependencies directly with the project, forge can run agnostically.
