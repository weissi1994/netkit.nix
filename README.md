# netkit.nix
Versatile icebox plugins for advanced networking scenarios in NixOS.

# What is it?
Intended to work out-of-box without any complicated configuration, `netkit.nix` is a set of [icebox](https://github.com/icebox-nix/icebox) purely declarative plugins for networking scenarios, such as versatile transparent proxy, sharing Wi-Fi through Wi-Fi.

# How to use it?
1. Add `netkit` to flake using `inputs.netkit.url = "github:icebox-nix/netkit.nix";`.
2. Add respective modules (like `netkit.nixosModules.clash`) to your `flake.nix`'s `nixosConfiguration.modules` list.
3. Configure modules on your needs. For details, see [wiki page](https://github.com/icebox-nix/netkit.nix/wiki).
```nix
netkit = {
   clash = {
     enable = true;
     redirPort =
       7892; # This must be the same with the one in your clash.yaml
   };

   wifi-relay = {
     interface = "wlp0s20f3"; # Change according to your device
     ssid = "netkit.nix";
     passphrase = "88888888";
   };

   xmm7360 = {
	 enable = true;
     autoStart = true;
     config = {
       mycard = {
         apn = "3gnet";
         nodefaultroute = false;
         noresolv = true;
       };
     };
     package = pkgs.xmm7360-pci_5_7;
   };
};
```

# List of plugins available
- [Clash](https://github.com/Dreamacro/clash) (`plugins/clash`): transparent proxy module with separated maxmind-geoip package and [yacd](https://github.com/haishanh/yacd) dashboard built-in.
- wifi-relay (`plugins/wifi-relay`): Sharing Wi-Fi connection over Wi-Fi on supported devices using `hostapd` and `dhcpd`.
- [snapdrop](https://github.com/RobinLinus/snapdrop): Cross-platform Apple AirDrop alternative.
- [frpc](https://github.com/fatedier/frp): A fast reverse proxy to help you expose a local server behind a NAT or firewall to the internet.
- minecraft-server: On-demand minecraft server with more options.
- [xmm7360](https://github.com/xmm7360/xmm7360-pci): A module with service for setting up PCI driver for Fibocom L850-GL modem (PCI ID 8086:7360).
