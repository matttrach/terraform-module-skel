# Terraform Module Skeleton

This module skeleton provides a base to start developing a new module using the same paradigms as other modules.
WARNING! Change the tests/go.mod to the new module name!

This is an "Independent" module, please see [terraform.md](./terraform.md) for more information.

## Requirements

### Nix

These modules use Nix the OS agnostic package manager to install and manage local package dependencies,
 install Nix and source the .envrc to enter the environment.
The .envrc will load a Nix development environment (a Nix shell), using the flake.nix file.
You can easily add or remove dependencies by updating that file, the flake.lock is a lock file to cache dependencies.
After loading the Nix shell, Nix will source the .envrc, setting all of the environment variables as necessary.
This is a way to resolve "works on my machine" issues, if you would prefer to install the local requirements on your machine, this module will work without modification.
Simply install the same requirements in the flake.nix and everything will work.

## Other Requirement

This is usually not a software requirement, but an account or a config file expected to exist on the local machine.

## Local State

The specific use case for the example modules here is temporary infrastructure for testing purposes.
With that in mind it is not expected that the user will manage the resources as a team, therefore the state files are all stored locally.
If you would like to store the state files remotely, add a terraform backend file (`*.name.tfbackend`) to your implementation module.
https://www.terraform.io/language/settings/backends/configuration#file

## Override Tests

You may want to test this code with slightly different parameters for your environment.
Check out [Terraform override files](https://developer.hashicorp.com/terraform/language/files/override) as a clean way to modify the inputs without accidentally committing any personalized code.

## Testing

I test manually on a 2019 MacBook Pro with Intel i7 on Ventura.

- I use nix that I have installed using brew
- I use direnv that I have installed using brew
- I simply use `direnv allow` to enter the environment
- I navigate to the `test` directory and run `go test .`
- I use `override.tf` files to change the values of `examples` to personalized data so that I can run them

Our continuous integration tests in a NixOS container and manually sources the `.envrc` to provide a very similar environment.
