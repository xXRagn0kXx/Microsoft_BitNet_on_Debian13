# BitNet_On_Debian13

![Portada de BitNet_Debian](BitNet_Debian.png)


# 1 Instalar software necesario
```bash
apt update
```
```bash
apt install lsb-release wget gnupg python3 python3-venv python3-dev python3-pip build-essential cmake clang git curl
```
# 2 Bajar compilador
BitNet requiere Clang versión 18 o superior para compilar correctamente su núcleo en C++. Debian 13 no trae versiones tan recientes por defecto, así que necesitas obtenerlas desde el repositorio oficial de LLVM.	 
Como root:

```bash
bash -c "$(wget -O - https://apt.llvm.org/llvm.sh)"
```

# 3 Miniconda

Ejecutamos con el usuario bitnet para que miniconda se instale en /home/bitnet/:
```bash
wget https://repo.anaconda.com/miniconda/Miniconda3-latest-Linux-x86_64.sh
```
```bash
bash Miniconda3-latest-Linux-x86_64.sh
```

Tendremos que aceptar el acuerdo de licencia y confirmar el directorio a elejir:

```bash
Do you accept the license terms? [yes|no]
>>> yes

Miniconda3 will now be installed into this location:
/home/bitnet/miniconda3


  - Press ENTER to confirm the location
  - Press CTRL-C to abort the installation
  - Or specify a different location below
```

Nos preguntara si deseamos automatizar el inicio de conda en la shell
:warning: Si respondes "yes", el instalador modificará tu archivo de configuración del shell (como ~/.bashrc, ~/.zshrc, etc.) para que se cargue automáticamente Conda cada vez que abras una terminal.
Si elijes "No" puedes activarlo manualmente solo cuando lo necesites, usando:
```bash
source ~/miniconda3/bin/activate
```
Para que los cambios hagan efecto si hemos elejido YES bastara con salir y entrar de la shell.
```bash
You can undo this by running `conda init --reverse $SHELL`? [yes|no]
[no] >>> yes
no change     /home/bitnet/miniconda3/condabin/conda
no change     /home/bitnet/miniconda3/bin/conda
no change     /home/bitnet/miniconda3/bin/conda-env
no change     /home/bitnet/miniconda3/bin/activate
no change     /home/bitnet/miniconda3/bin/deactivate
no change     /home/bitnet/miniconda3/etc/profile.d/conda.sh
no change     /home/bitnet/miniconda3/etc/fish/conf.d/conda.fish
no change     /home/bitnet/miniconda3/shell/condabin/Conda.psm1
no change     /home/bitnet/miniconda3/shell/condabin/conda-hook.ps1
no change     /home/bitnet/miniconda3/lib/python3.13/site-packages/xontrib/conda.xsh
no change     /home/bitnet/miniconda3/etc/profile.d/conda.csh
modified      /home/bitnet/.bashrc

==> For changes to take effect, close and re-open your current shell. <==

Thank you for installing Miniconda3!
```

# 4 Crear entorno conda

Activamos la shell de conda si no lo esta:
```bash
source ~/miniconda3/bin/activate
```
Se quedara algo como:
```bash
(base) bitnet@BitNet:~$ 
```
Creamos el entorno en esa shell:
```bash
conda create -n miniconda-bitnet-p3_9 python=3.9
```

Tendremos que aceptar los terminos de servicio:
```bash
Do you accept the Terms of Service (ToS) for https://repo.anaconda.com/pkgs/main? [(a)ccept/(r)eject/(v)iew]: a
```
Nos mostrara todos los paquetes a descargar e instalar, confirmamos con "y"
```bash
The following packages will be downloaded:
   |-------------------------------------------------------------|
   | package                    |            build               |
   |----------------------------|--------------------------------|
   | pip-25.2                   |     pyhc872135_0         1.2 MB|
   | python-3.9.23              |       he99959a_0        24.7 MB|
   | setuptools-78.1.1          |   py39h06a4308_0         1.7 MB|
   | wheel-0.45.1               |   py39h06a4308_0         114 KB|
   |-------------------------------------------------------------|
                                           Total:        27.7 MB

The following NEW packages will be INSTALLED:

  _libgcc_mutex      pkgs/main/linux-64::_libgcc_mutex-0.1-main
  _openmp_mutex      pkgs/main/linux-64::_openmp_mutex-5.1-1_gnu
  bzip2              pkgs/main/linux-64::bzip2-1.0.8-h5eee18b_6
  ca-certificates    pkgs/main/linux-64::ca-certificates-2025.7.15-h06a4308_0
  expat              pkgs/main/linux-64::expat-2.7.1-h6a678d5_0
  ld_impl_linux-64   pkgs/main/linux-64::ld_impl_linux-64-2.40-h12ee557_0
  libffi             pkgs/main/linux-64::libffi-3.4.4-h6a678d5_1
  libgcc-ng          pkgs/main/linux-64::libgcc-ng-11.2.0-h1234567_1
  libgomp            pkgs/main/linux-64::libgomp-11.2.0-h1234567_1
  libstdcxx-ng       pkgs/main/linux-64::libstdcxx-ng-11.2.0-h1234567_1
  libxcb             pkgs/main/linux-64::libxcb-1.17.0-h9b100fa_0
  ncurses            pkgs/main/linux-64::ncurses-6.5-h7934f7d_0
  openssl            pkgs/main/linux-64::openssl-3.0.17-h5eee18b_0
  pip                pkgs/main/noarch::pip-25.2-pyhc872135_0
  pthread-stubs      pkgs/main/linux-64::pthread-stubs-0.3-h0ce48e5_1
  python             pkgs/main/linux-64::python-3.9.23-he99959a_0
  readline           pkgs/main/linux-64::readline-8.3-hc2a1206_0
  setuptools         pkgs/main/linux-64::setuptools-78.1.1-py39h06a4308_0
  sqlite             pkgs/main/linux-64::sqlite-3.50.2-hb25bd0a_1
  tk                 pkgs/main/linux-64::tk-8.6.15-h54e0aa7_0
  tzdata             pkgs/main/noarch::tzdata-2025b-h04d1e81_0
  wheel              pkgs/main/linux-64::wheel-0.45.1-py39h06a4308_0
  xorg-libx11        pkgs/main/linux-64::xorg-libx11-1.8.12-h9b100fa_1
  xorg-libxau        pkgs/main/linux-64::xorg-libxau-1.0.12-h9b100fa_0
  xorg-libxdmcp      pkgs/main/linux-64::xorg-libxdmcp-1.1.5-h9b100fa_0
  xorg-xorgproto     pkgs/main/linux-64::xorg-xorgproto-2024.1-h5eee18b_1
  xz                 pkgs/main/linux-64::xz-5.6.4-h5eee18b_1
  zlib               pkgs/main/linux-64::zlib-1.2.13-h5eee18b_1


Proceed ([y]/n)?
```

Una vez instalado nos dara lagunas instruciones para activar o desactivar la shell de conda:
```bash
Downloading and Extracting Packages:

Preparing transaction: done
Verifying transaction: done
Executing transaction: done
#
# To activate this environment, use
#
#     $ conda activate miniconda-bitnet-p3_9
#
# To deactivate an active environment, use
#
#     $ conda deactivate
```
## 4.1 Activar conda

conda activate miniconda-bitnet-p3_9

Nos cambiara el promp de la terminal  con el nombre de miniconda-bitnet-p3_9
NOTA: ESTO SERA NECESARIO CADA VEZ QUE QUERRAMOS EJEUTAR EL MODELO
Ej:
```bash
(base) bitnet@BitNet:~$ conda activate miniconda-bitnet-p3_9
(miniconda-bitnet-p3_9) bitnet@BitNet:~$
```
# 5 Descargar Bitnet 
```bash
git clone --recursive https://github.com/microsoft/BitNet.git
```
Entramos al directorio nuevo generado: 
```bash
cd BitNet
```
# 6 Instalar dependencias de python para el modelo:
```bash
pip install -r requirements.txt
```
Ahora forzaremos a setup_env.py a usar Clang 19 como compilador en lugar del predeterminado del sistema (que suele ser gcc o una versión más antigua de clang).

⚠️ Sin esto:
El script puede usar un compilador incorrecto por defecto (como gcc o clang-14) que no soporta completamente las extensiones modernas de C++ requeridas por BitNet.

En Debian 13, clang-19 no es el compilador predeterminado, aunque lo hayas instalado tendremos que ejecutar:
```bash
export CC=/usr/bin/clang-19
export CXX=/usr/bin/clang++-19
```
# 7 Bajamos y compilamos el modelo 

Dentro de la ruta /home/usuario/BitNet ejecutamos: 

Descargar modelo:
# Este comando ya esta deprecado, seria para versiones antiguas:
# huggingface-cli download microsoft/BitNet-b1.58-2B-4T-gguf --local-dir models/BitNet-b1.58-2B-4T
Actual:
```bash
hf download microsoft/BitNet-b1.58-2B-4T-gguf --local-dir models/BitNet-b1.58-2B-4T
```

Compilar el modelo con cuantizacion I2_S(RAM recomendada 4–6 GB):
```bash
python setup_env.py -md models/BitNet-b1.58-2B-4T -q i2_s
```
Compilar el modelo con cuantizacion TL2 (RAM recomendada 10–16 GB):
```bash
python setup_env.py -md models/BitNet-b1.58-2B-4T -q tl2
```
# 8 Ejecutar modelo

Si es i2_s
```bash
python run_inference.py -m models/BitNet-b1.58-2B-4T/ggml-model-i2_s.gguf -cnv -p "lo que le queramos preguntar"
```
Si es TL2
```bash
python run_inference.py -m models/BitNet-b1.58-2B-4T/ggml-model-tl2.gguf -cnv -p "lo que le queramos preguntar"
```
