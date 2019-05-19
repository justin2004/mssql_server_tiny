# mssql_server_tiny

## what
- a slightly modified Microsoft SQL Server docker image
    - modified to allow execution on a machine with less than 2 GiB of physical memory

## why
- Microsoft's sqlservr, at startup, looks to see how much physical memory its host has
- if the host has less than 2 GiB sqlservr just quits with the message:
    - "sqlservr: This program requires a machine with at least 2000 megabytes of memory."
- it turns out that sqlservr does not try to allocate that much memory and fail but rather sqlservr enforces that as a policy (perhaps to cut down on performance related issues due to page faulting)
- but i think if someone wants to use swap space instead of physical memory that is up to that person


## how
- using LD_PRELOAD to redefine the system call "sysinfo"
- when sqlservr invokes the "sysinfo" system call (to see how much physical memory the host has) we instead lie to sqlservr with our redefined sysinfo function




- `https://hub.docker.com/_/microsoft-mssql-server`
- `https://github.com/Microsoft/mssql-docker`



