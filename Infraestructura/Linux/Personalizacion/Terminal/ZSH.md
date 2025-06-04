## **📥 1. Instalar Zsh** (si no está instalado)

```bash
sudo pacman -S zsh zsh-completions
```

#### **Hacer Zsh tu shell por defecto**:

```bash
chsh -s $(which zsh)
```

Reinicia la terminal.

---

## **⚡ 2. Instalar Oh My Zsh**

```bash
sh -c "$(curl -fsSL https://raw.githubusercontent.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"
```

#### **zsh-syntax-highlighting**

```bash
git clone https://github.com/zsh-users/zsh-syntax-highlighting.git ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-syntax-highlighting
``` 

#### **zsh-autosuggestions**

```bash
git clone https://github.com/zsh-users/zsh-autosuggestions ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-autosuggestions
```

## **🎨 3. Instalar Powerlevel10k (Tema)**

```bash
git clone --depth=1 https://github.com/romkatv/powerlevel10k.git ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/themes/powerlevel10k
```

#### **Configurar el tema en `~/.zshrc`**:

```bash
nano ~/.zshrc
```

Cambia esta línea:

```zsh
ZSH_THEME="powerlevel10k/powerlevel10k"

```
Guarda (`Ctrl+O` → `Enter` → `Ctrl+X`) y recarga:

```bash
source ~/.zshrc
```

Sigue el asistente interactivo (`p10k configure`) para personalizar el prompt.

---

## **🔌 4. Instalar Plugins Esenciales**

### **A. zsh-autosuggestions** (sugerencias de comandos)

```bash
git clone https://github.com/zsh-users/zsh-autosuggestions ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-autosuggestions
```

### **B. zsh-syntax-highlighting** (resaltado de sintaxis)

```bash
git clone https://github.com/zsh-users/zsh-syntax-highlighting.git ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-syntax-highlighting
```

---

## **⚙️ 5. Configurar Plugins en `~/.zshrc`**

Edita el archivo:

```bash
nano ~/.zshrc
```

Busca la línea `plugins=` y añade los plugins:

```zsh
plugins=(
  git
  zsh-autosuggestions
  zsh-syntax-highlighting
)

```

---



---

## **🔄 7. Recargar Configuración**

```bash
source ~/.zshrc
```

---

## **🎉 Resultado Final**

- **Prompt**: Powerlevel10k con iconos y colores personalizados.
    
- **Autocompletado**: Sugerencias grises (`zsh-autosuggestions`).
    
- **Resaltado**: Comandos válidos/inválidos en verde/rojo (`zsh-syntax-highlighting`).