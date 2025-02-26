---
Created: Invalid date
Updated: Invalid date
---
- Install pre-requisites

https://www.microsoft.com/net/core\#macos

brew update

brew install openssl

mkdir -p /usr/local/lib

ln -s /usr/local/opt/openssl/lib/libcrypto.1.0.0.dylib /usr/local/lib/

ln -s /usr/local/opt/openssl/lib/libssl.1.0.0.dylib /usr/local/lib/

- install .NET Core SDK

https://go.microsoft.com/fwlink/?linkid=843444  <- install link

ln -s /usr/local/share/dotnet/dotnet /usr/local/bin

https://github.com/dotnet/core/blob/master/cli/known-issues.md

- initialize some code

dotnet new console -o hwapp

cd hwapp

- run the app

dotnet restore

dotnet run