# calamares-packagechooser
Implementation for Community Edition installs with calamares packagechooser module

## How to get my Community Edition added into EndeavourOS installer?

1. To use the packagechooser module in calamares we need you to add your Community Edition into the needed configuration files for calamares:
* https://github.com/endeavouros-team/calamares_config_next/blob/master/calamares/modules/packagechooser.conf
* https://github.com/endeavouros-team/calamares_config_next/blob/master/calamares/modules/

2. add the packages list that is needed in addition to the base system you find in this file: *netinstall-ce-base.yaml** here:
* https://github.com/endeavouros-team/calamares_config_next/tree/master/calamares/ce
File name is your **id** used in **packagechooser.conf** that will be used to select and install the packages list inside the **contextualprocess.conf**

3. add a screenshot for your Community Edition here:
* https://github.com/endeavouros-team/calamares_config_next/tree/master/calamares/images

# packagechooser.conf

```
    - id: sway
      name: "Sway Edition"
      description: "Sway Community Edition. Sway is a tiling Wayland compositor and a drop-in replacement for the i3 window manager for X11. Sway allows you to arrange your application windows logically, rather than spatially. Windows are arranged into a grid by default which maximizes the efficiency of your screen and can be quickly manipulated using only the keyboard."
      description[de]: "Sway-Community-Edition. Sway ist ein Wayland-Kompositor mit Kacheln und ein Drop-In-Ersatz für den i3-Fenstermanager für X11. Mit Sway können Sie Ihre Anwendungsfenster logisch und nicht räumlich anordnen. Fenster sind standardmäßig in einem Raster angeordnet, das die Effizienz Ihres Bildschirms maximiert und schnell nur mit der Tastatur manipuliert werden kann."
      description[fr]: "Édition communautaire Sway. Sway est un compositeur de carrelage Wayland et un remplacement instantané du gestionnaire de fenêtres i3 pour X11. Sway vous permet d'organiser vos fenêtres d'application de manière logique plutôt que spatiale. Les fenêtres sont organisées par défaut dans une grille qui maximise l'efficacité de votre écran et peut être rapidement manipulée en utilisant uniquement le clavier."
      description[it]: "Sway edizione comunitaria. Sway è un compositore di piastrelle Wayland e un sostituto drop-in per il gestore di finestre i3 per X11. Sway consente di organizzare le finestre dell'applicazione in modo logico, anziché spaziale. Le finestre sono organizzate in una griglia per impostazione predefinita che massimizza l'efficienza dello schermo e può essere rapidamente manipolata utilizzando solo la tastiera."
      description[sp]: "Sway Community Edition. Sway es un compositor de Wayland en mosaico y un reemplazo directo del administrador de ventanas i3 para X11. Sway le permite organizar las ventanas de su aplicación de forma lógica, en lugar de espacialmente. Las ventanas están organizadas en una cuadrícula de forma predeterminada, lo que maximiza la eficiencia de su pantalla y se puede manipular rápidamente usando solo el teclado."
      description[ru]: "Sway Community Edition. Sway - это мозаичный композитор Wayland, который заменяет оконный менеджер i3 для X11. Sway позволяет вам упорядочивать окна приложений логически, а не пространственно. По умолчанию окна объединены в сетку, что обеспечивает максимальную эффективность экрана, и ими можно быстро управлять, используя только клавиатуру."
      description[zh_CN]: "Sway 社区版。 Sway 是一个平铺的 Wayland 合成器，是 X11 的 i3 窗口管理器的替代品。 Sway 允许您以逻辑方式而非空间方式排列应用程序窗口。默认情况下，Windows 排列成一个网格，这可以最大限度地提高屏幕效率，并且可以仅使用键盘进行快速操作。"
      description[ja]: "スウェイコミュニティエディション。 Swayは、タイリングWaylandコンポジターであり、X11用のi3ウィンドウマネージャーのドロップイン代替品です。 Swayを使用すると、アプリケーションウィンドウを空間的ではなく論理的に配置できます。ウィンドウはデフォルトでグリッドに配置されているため、画面の効率が最大になり、キーボードのみを使用してすばやく操作できます。"
      screenshot: "/etc/calamares/images/sway.jpg"
```

Translations are not required  but should be good to make it clear for everyone what your setup is about.

```
    - id: sway
      name: "Sway Edition"
      description: "text text text"
      screenshot: "/etc/calamares/images/sway.jpg"
 ```

This 4 ones are requiered to add your Edition. Please validate your edit with a yaml validator! The 2 calamares config files must be valid yaml to be used.

Screenshot should have 1067x800 pixels and must be .jpg
<img src="https://raw.githubusercontent.com/endeavouros-team/calamares_config_next/master/calamares/images/sway.jpg" alt="example" width="1067"/>

# contextualprocess.conf:

```
# SPDX-FileCopyrightText: no
# SPDX-License-Identifier: CC0-1.0
#
# Configuration for running chosen Community Editions package install
#
---
dontChroot: false
timeout: 600

packagechooser_packagechooser:

    sway:   "pacman -Sy --needed --noconfirm - < /tmp/ce/sway.txt"
    
    bspwm:  "pacman -Sy --needed --noconfirm - < /tmp/ce/bspwm.txt"
 
i18n:
 name: "installing package list for chosen Community Edition..."
 name[de]: "Paketliste für ausgewählte Community Edition installieren..."
 name[fr]: "installation de la liste des packages pour l'édition communautaire choisie..."
 name[it]: "installazione dell'elenco dei pacchetti per la Community Edition scelta..."
 name[es]: "instalación de la lista de paquetes para la Community Edition elegida ..."
 name[ru]: "установка списка пакетов для выбранного Community Edition ..."
 name[zh_CN]: "安装所选社区版的软件包列表..."
 name[ja]: "選択したCommunityEditionのパッケージリストをインストールしています..."
```
   
   
 `sway:   "pacman -Sy --needed --noconfirm - < /tmp/ce/sway.txt"`
 
 Where sway is the **id:** and **sway.txt** is the packages list.
 
 4. create a PKGBUILD that installs your configs to /etc/skel and may runs a config script on first boot to setup user specific stuff
# PKGBUILD:
```
# Maintainer: Aryan <aryanpothu@tutanota.com>
# Contributor: joekamprad <joekamprad@endeavouros.com>
# Contributor: The-Repo-Club <The-Repo-Club@github.com>

_pkgname=sway
pkgname=eos-skel-ce-sway
pkgver=1.0
pkgrel=1
pkgdesc="pre user creation skel setup for SWAY EOS-CE"
arch=('any')
groups=('eos-ce')
url="https://github.com/EndeavourOS-Community-Editions/${pkgname}"
license=('GPL')
conflicts=('eos-ce-sway')
depends=('git')
source=("${_pkgname}::git+https://github.com/EndeavourOS-Community-Editions/${_pkgname}.git")
sha256sums=('SKIP')

package() {
    PREFIX=/etc/skel
    cd "$_pkgname"
    mkdir -p "${pkgdir}${PREFIX}/.config/"
    cp -R ".config/" "${pkgdir}${PREFIX}/"
    install -Dm644 ".gtkrc-2.0" "${pkgdir}${PREFIX}/.gtkrc-2.0"
    install -Dm644 ".profile" "${pkgdir}${PREFIX}/.profile"
    install -Dm644 ".nanorc" "${pkgdir}${PREFIX}/.nanorc"
    install -Dm755 "set_once.sh" "${pkgdir}${PREFIX}/set_once.sh"
    install -Dm644 "xed.dconf" "${pkgdir}${PREFIX}/xed.dconf"
}
```
And create a pull request to add it to the EndeavourOS repository. this package must be added to your packages list too.

The Structure of your dotfiles should be sorted like this:

* https://github.com/EndeavourOS-Community-Editions/sway
* 
So it can be used by the PKGBUILD in the above example.

You do not need to use GitHub any other place can be used also to develop your repo, but to be added to installer we need a copy here at this repository.
