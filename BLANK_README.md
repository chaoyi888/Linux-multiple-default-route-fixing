<!--
*** Thanks for checking out the Best-README-Template. If you have a suggestion
*** that would make this better, please fork the repo and create a pull request
*** or simply open an issue with the tag "enhancement".
*** Thanks again! Now go create something AMAZING! :D
***
***
***
*** To avoid retyping too much info. Do a search and replace for the following:
*** github_username, repo_name, twitter_handle, email, project_title, project_description
-->



<!-- PROJECT SHIELDS -->
<!--
*** I'm using markdown "reference style" links for readability.
*** Reference links are enclosed in brackets [ ] instead of parentheses ( ).
*** See the bottom of this document for the declaration of the reference variables
*** for contributors-url, forks-url, etc. This is an optional, concise syntax you may use.
*** https://www.markdownguide.org/basic-syntax/#reference-style-links

<!-- GETTING STARTED -->
## Getting Started

There are only a few scenarios, such as when using multipath TCP, in which you require multiple default gateways on a host. In most cases, you configure only a single default gateway to avoid unexpected routing behavior or asynchronous routing issues.

**NOTE**
To route traffic to different internet providers, use policy-based routing instead of multiple default gateways.

### Prerequisites

1. The host uses NetworkManager to manage network connections, which is the default.
2. The host has multiple network interfaces.
3. The host has multiple default gateways configured.

### Procedure

1. Display the routing table:
   * For IPv4, enter:
     ```sh
     # ip -4 route
     default via 192.0.2.1 dev enp1s0 proto static metric 101
     default via 198.51.100.1 dev enp7s0 proto static metric 102
     ...
     ```
   * For IPv6, enter:
     ```sh
     # ip -6 route
     default via 2001:db8:1::1 dev enp1s0 proto static metric 101 pref medium
     default via 2001:db8:2::1 dev enp7s0 proto static metric 102 pref medium
     ...
     ```
   Entries starting with default indicate a default route. Note the interface names of these entries displayed next to dev.
   
2. Use the following commands to display the NetworkManager connections that use the interfaces you identified in the previous step:
     ```sh
    # nmcli -f GENERAL.CONNECTION,IP4.GATEWAY,IP6.GATEWAY device show enp1s0
    GENERAL.CONNECTION:      Corporate-LAN
    IP4.GATEWAY:             192.168.122.1
    IP6.GATEWAY:             2001:db8:1::1

    # nmcli -f GENERAL.CONNECTION,IP4.GATEWAY,IP6.GATEWAY device show enp7s0
    GENERAL.CONNECTION:      Internet-Provider
    IP4.GATEWAY:             198.51.100.1
    IP6.GATEWAY:             2001:db8:2::1
     ```
    In these examples, the profiles named Corporate-LAN and Internet-Provider have the default gateways set. Because, in a local network, the default gateway is typically the host that is one hop closer to the internet, the rest of this procedure assumes that the default gateways in the Corporate-LAN are incorrect.

3. Configure that NetworkManager does not use the Corporate-LAN connection as the default route for IPv4 and IPv6 connections:
     ```sh
    # nmcli connection modify Corporate-LAN ipv4.never-default yes ipv6.never-default yes
     ```
   Note that setting ipv4.never-default and ipv6.never-default to yes, automatically removes the default gateway’s IP address for the corresponding protocol from the connection profile.

4. Activate the Corporate-LAN connection:
     ```sh
    # nmcli connection up Corporate-LAN
     ```

5. Verification steps
    * Display the IPv4 and IPv6 routing tables and verify that only one default gateway is available for each protocol:
        ** For IPv4, enter:
            ```sh
            # ip -4 route
            default via 192.0.2.1 dev enp1s0 proto static metric 101
            ...
            ```








<!-- USAGE EXAMPLES -->
## Usage

Use this space to show useful examples of how a project can be used. Additional screenshots, code examples and demos work well in this space. You may also link to more resources.

_For more examples, please refer to the [Documentation](https://example.com)_



<!-- ROADMAP -->
## Roadmap

See the [open issues](https://github.com/github_username/repo_name/issues) for a list of proposed features (and known issues).



<!-- CONTRIBUTING -->
## Contributing

Contributions are what make the open source community such an amazing place to be learn, inspire, and create. Any contributions you make are **greatly appreciated**.

1. Fork the Project
2. Create your Feature Branch (`git checkout -b feature/AmazingFeature`)
3. Commit your Changes (`git commit -m 'Add some AmazingFeature'`)
4. Push to the Branch (`git push origin feature/AmazingFeature`)
5. Open a Pull Request



<!-- LICENSE -->
## License

Distributed under the MIT License. See `LICENSE` for more information.



<!-- CONTACT -->
## Contact

Your Name - [@twitter_handle](https://twitter.com/twitter_handle) - email

Project Link: [https://github.com/github_username/repo_name](https://github.com/github_username/repo_name)



<!-- ACKNOWLEDGEMENTS -->
## Acknowledgements

* []()
* []()
* []()





<!-- MARKDOWN LINKS & IMAGES -->
<!-- https://www.markdownguide.org/basic-syntax/#reference-style-links -->
[contributors-shield]: https://img.shields.io/github/contributors/github_username/repo.svg?style=for-the-badge
[contributors-url]: https://github.com/github_username/repo/graphs/contributors
[forks-shield]: https://img.shields.io/github/forks/github_username/repo.svg?style=for-the-badge
[forks-url]: https://github.com/github_username/repo/network/members
[stars-shield]: https://img.shields.io/github/stars/github_username/repo.svg?style=for-the-badge
[stars-url]: https://github.com/github_username/repo/stargazers
[issues-shield]: https://img.shields.io/github/issues/github_username/repo.svg?style=for-the-badge
[issues-url]: https://github.com/github_username/repo/issues
[license-shield]: https://img.shields.io/github/license/github_username/repo.svg?style=for-the-badge
[license-url]: https://github.com/github_username/repo/blob/master/LICENSE.txt
[linkedin-shield]: https://img.shields.io/badge/-LinkedIn-black.svg?style=for-the-badge&logo=linkedin&colorB=555
[linkedin-url]: https://linkedin.com/in/github_username
