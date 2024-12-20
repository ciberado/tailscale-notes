[](#title,.coverbg)

# HomeLab with Tailscale, Docker and AWS

![HomeLab](images/homelab.jpg)

[](.coverbg.topic)

## Who am I?

[](.coverbg.headrd)

### Javi Moreno

![Jean Luc Picard portrait](images/picard.jpg)

::: Notes

email at javier-moreno dt com

:::

[](.coverbg)

### Principal Cloud Consultant

![NTT Data logo](images/ntt-logo.png)

[](.coverbg)

### Postgraduate Course co-Director

![UPCSchool cloud course](images/upcschool.png)

::: Notes

You can find more information about the course at its
[web]() or by asking me :)

:::

[](.coverbg.topic)

## HomeLab

[](.coverbg)

### What?

![A cardboard server](images/homelab-cardboard-server.png)

::: Notes

It is the opposite to a professional infrastructure.
A HomeLab is a set of compute resources that you can **break** unexpectedly,
but that works most of the time.

:::

[](.coverbg)

### Why?

![Girl Playing Inside Her Room, by Tatiana Syrikova, https://www.pexels.com/photo/girl-playing-inside-her-room-3933025/](images/pexels-tatianasyrikova-3933025.jpg)

::: Notes

Fun. Learn. Comfort. Profit?

![A party of cardboards servers](images/homelab-cardboard-party.png)

:::

[](.coverbg)

### How?

![A laptop](images/msi-gt72-vr-tequila.jpg)

::: Notes

Meet Tequila, a MSI gt72 Dominator Pro
with a GTX 1060 with 3GB VRAM and 16GB RAM.
3.8Kg of mobile (more or less) computer.

:::

[](.coverbg)

### Where

![A picture of living room furniture](images/comedor.jpg)

[](.coverbg.topic)

## Regular services

[](.coverbg.screenshot)

### Photos with [Immich](https://immich.app/)

![A screenshot of Immich](images/immich.png)

[](.coverbg.screenshot)

### IoT with [Home Assistant](https://www.home-assistant.io/)

![a screenshot of Home Assistant](images/ha.png)

[](.coverbg.screenshot.dark)

### Media management with [Jellyfin](https://jellyfin.org/)

![A screenshot of Jellyfin](images/jellyfin.png)

[](.coverbg.screenshot)

### Quizzes with [Quizi](https://github.com/cosmoart/quiz-game)

![A screenshot of Quizi](images/quizi.png)

::: Notes

We use quizzes a lot in the postgraduate course, as it is the
most effective way of fixing concepts in long-term memory by
practicing [spaced repetition](https://www.amazon.es/Make-Stick-Science-Successful-Learning/dp/0674729013).

Unfortunately, the tool we used for it has changed its
terms and conditions, so I'm looking for a replacement.
During the following months, I plan to adapt 
[my fork](https://github.com/ciberado/quiz-game)
of the original Quizi to fill this role.
:::

[](.coverbg.topic)

## Advanced services

[](.coverbg.screenshot)

### Image generation with [Fooocus](https://github.com/lllyasviel/Fooocus)

![A Fooocus github repo screenshot](images/fooocus.png)

[](.coverbg)

### LLM with [Ollama](https://ollama.com)

![A screenshot of the Ollama website](images/ollama.png)

::: Notes

g5.12xlarge (96GB VRAM) with Llama 2 90B generates 2 tokens/s with a input context of 2500 tokens, as
explained in [Benchmarking Llama 2 70B inference on AWS’s g5.12xlarge vs an A100](https://medium.com/@krohling/benchmarking-llama-2-70b-inference-on-awss-g5-12xlarge-vs-an-a100-9d387d969177), at $2 per hour.

g4dn.xlarge (16GB VRAM) at spot costs $0.16 per hour, being able to fluently run smaller models, Whisper large, etc.

:::

[](.coverbg.topic)

## Challenges

[](.coverbg)

### Remote access

![A man using a smartphone, by Sanket Mishra, https://www.pexels.com/photo/young-man-using-smartphone-on-public-transport-28461205/](images/pexels-sanketgraphy-28461205.jpg)

::: Notes

From my parent's house, from our phones.

:::

[](.coverbg)

### Resources

![A NVidia A100](images/nvidia-a100.png)

::: Notes

I think VRAM is the biggest limitation in a home scenario.
This NVidia A100 with 80GB costs around $10K. WTF.

:::

[](.coverbg.topic)

## Solution: AWS

[](.coverbg)

### Challenge: connectivity price

![A picture of Scrooge McDuck](images/tio-gilito.png)

::: Notes

Public endpoints require multiple subnets, NATgw, public IPs, ALB... 
and we haven't even talked about the EC2 instances. It all adds up.
AWS's first source of income are NATgw, probably.

:::

[](.coverbg)

### Challenge: connectivity complexity

![A guy holding many wires](images/wires-wires.png)

::: Notes

I mean, why was I doing this? This is a HomeLab, not an Enterprise 
Architecture. It was supposed to be fun! **I already have a job**.

:::

[](.coverbg.topic)

## Introducing Tailscale

[](.coverbg.screenshot)

### Company history

![Tailscale staff](images/tailscale-people.png)

::: Notes

* Founded in 2019 in Ontario by ex-googlers Avery Pennarun, David Carney and Brad Fitzpatrick 
* Small and medium sized enterprise (around 80 employees)
* Focused in one product

::: Notes


[](#mesh,.illustration)

### Product technology

![Diagram of a mesh, from Tailscape docs](images/mesh.png)

* Overlay network (tailnet)
* UDP peer-to-peer VPN
* Wireguard-based 
* Open source client
* Free for 3 users / 100 devices
* [Alternative](https://headscale.net/) control plane available

::: Notes

* Overlay approach is portable.
* Peer means efficient.
* Wireguard is open source and battle tested.

:::

[](.coverbg.screenshot)

### [Account creation](https://tailscale.com/)

![Tailscale login page](images/login.png)

::: Notes

Use your preferred IdP.

:::

[](.illustration)

### [Tailnet configuration](https://login.tailscale.com/admin/dns)

![Three numbers in a row, by Magda Ehlers, https://www.pexels.com/photo/blue-red-and-yellow-stripe-surface-1329297/](images/one-two-three.png)

* Rename the tailnet
* Activate MagicDNS
* Activate automatic HTTPs certificates

::: Notes

One user will be associated to one tailnet, but devices can be shared between tailnets.

:::

[](.coverbg.screenshot)

### Client install

![OS logos](images/os-logos.png)

::: Notes

Next, next, next finish.

Windows, Linux, MacOS, Android, Chromebooks, Google TV, iOS, Apple TV.

:::

[](.coverbg)

### Device configuration

![Magic meme](images/magic.png)

::: Notes

Many times, there is no node configuration, apart from providing authorization.

:::

[](.coverbg)

### Demo!

![A car going through an explosion](images/car-explosion.jpg)

::: Notes

Jump into an EC2 instance and install Tailscale:

```bash
curl -fsSL https://pkgs.tailscale.com/stable/ubuntu/noble.noarmor.gpg | sudo tee /usr/share/keyrings/tailscale-archive-keyring.gpg >/dev/null
curl -fsSL https://pkgs.tailscale.com/stable/ubuntu/noble.tailscale-keyring.list | sudo tee /etc/apt/sources.list.d/tailscale.list

sudo apt-get update
sudo apt-get install tailscale -y

sudo tailscale up --hostname=fooocus
```
:::

[](.coverbg.topic)

## Shared environment

[](.coverbg)

### Docker under WSL

![A screenshot of Vampire Survivors](images/vampire.png)

::: Notes

Tequila doubles as the family console, mostly for playing
[Vampire Surivors](https://store.steampowered.com/app/1794680/Vampire_Survivors/).
I'm way too old for investing time in hardware configuration,
so the machine is running Windows. That makes 
[WSL](https://learn.microsoft.com/en-us/windows/wsl/install)
the most natural way of starting containers. To make things
smoother, I've added a simple script for starting it every
time the computer is bootstrapped.

Just pres `Win+R`, type `shell:startup`, and drop it there
with the name `wsl-init.vbe`.

```vbe
Set ws = CreateObject("Wscript.Shell")
ws.run "wsl -d Ubuntu", vbhide
```

:::

[](.coverbg.screenshot)

### Docker compose approach

![A diagram explaining the three compose containers](images/compose-diagram.png)

::: Notes

The `nginx` container (that will provide the service name) just forwards
the TLS traffic to the actual server.

The tailscale container provides the network and the `tailscale` command.
It shares a volume with the `nginx` container, so it is possible to use
`tailscale cert` for automatically provision the https cert.

```yaml
services:
  - xxx-server    # The service image
  - ts-xxx        # The tailscale software
  - xxx           # A nginx proxy
```

:::

[](.topic)

## Features

[](.coverbg.screenshot.dark)

### Mobile access

![A screenshot of the immich app](images/immich-app.png)

::: Notes

Immich has a mobile App that can be used from a smartphone connected to the
tailnet.

:::

[](#quiz,.illustration)

### Public devices

[https://quiz.snow-burbot.ts.net](https://quiz.snow-burbot.ts.net)


![Quizi screenshot](images/quiz.png)

::: Notes



It is possible to use `tailnetd` as an HTTPs proxy, both internally and publicly.
That feature can be activate with the `serve` and `funnel` commands, or configured
using a `json` file like in the Quizz container device.
:::

[](.coverbg.screenshot.dark)

### Exit node

![The Netflix web](images/netflix.png)

::: Notes

Sets the gateway of one device to any other device configured to
work as *exit node*. It is also possible to integrate it with
[Mullvad VPN](https://mullvad.net).

This allows devices on other apartments to use your home IP,
fore example.

:::

[](.coverbg)

### Audited ssh

![A picture of a female ninja cat managing a computer](images/ninja-cat.png)

::: Notes

Once a device is configured for 
[accepting ssh connections](https://tailscale.com/kb/1193/tailscale-ssh)
through Tailscale, the authorized users will be able to
jump to that node using their Tailscale authentication,
and all the commands will be recorded for audit.

:::

[](.coverbg)

### Subnet propagation

![A datacenter connected to two wooden houses, by Bing](images/hybrid.png)

::: Notes

One node in the VPC with access to the internet can act as a subnet router, by
adding the `--advertise-routes` flag to the daemon configuration. The next step
consists in adding the [VPC DNS server to the tailnet](https://tailscale.com/kb/1141/aws-rds),
and that's all.

:::

[](.topic)

## Gotchas

[](.coverbg)

### Windows & WSL

![Two matrioskas dolls fighting each other](images/matrioskas.png)

::: Notes

You can run the Tailscale daemon in WSL and in containers at the same time.
But you can't run it on Windows and WSL: the responses don't reach the WSL daemon.

:::

[](.coverbg.screenshot.dark)

### WSL network propagation

![HA screenshot](images/ha-webapp.png)

::: Notes

A Mosquitto MQTT node resides in Tequila, but Tailscale 
on WSL seems to miss local network advertisement so the 
IoT devices in my home network are not able to access it. Running
Tailscale on them is out of question, so  to solve it I've set 
a bridge between the Windows host and te WSL port with

:::


[](#closing,.illustration)

### Closing words

![A qr code pointing to the github repo](images/qr-code.svg)

[tinyurl.com/tlscl](https://tinyurl.com/tlscl)

Perhaps it would be nice to evolve towards a world 
where we citizens also owned part of **our infrastructure**.