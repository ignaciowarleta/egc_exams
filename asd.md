# 🔐 Esquema de Kyber-KEM y su Relación con MLWE  

## 🏗 Paso 1: Bob Genera su Clave Pública y Privada (KeyGen - Basado en MLWE)  
Bob quiere recibir una clave segura de Alice, así que genera su par de claves:  

| **Bob (Receptor)** | **Acción** |
|--------------------|------------|
| 🔹 **Genera una matriz pública** \( A \) usando una semilla aleatoria. | \( A \in R_q^{k \times k} \) |
| 🔹 **Genera un vector secreto** \( s \) y un vector de error \( e \). | \( s, e \sim \beta_{\mu_1} (R_q^k) \) |
| 🔹 **Calcula la clave pública** \( b = A s + e \). | \( pk = (b, \text{seed}_A) \) |
| 🔹 **Clave privada:** \( sk = s \). | Se guarda en secreto. |

🔒 **Aquí el problema MLWE protege \( s \)**, ya que un atacante no puede resolver \( s \) a partir de \( A \) y \( b \) debido al error \( e \).

---

## 📩 Paso 2: Alice Encapsula una Clave Secreta (Encaps - Basado en MLWE)  
Alice quiere enviar una clave segura \( K \) a Bob.  

| **Alice (Emisora)** | **Acción** |
|---------------------|------------|
| 🔹 **Recrea la matriz** \( A \) a partir de \( \text{seed}_A \) de Bob. | \( A^T \) |
| 🔹 **Genera un vector aleatorio** \( r \) y errores \( e_1, e_2 \). | \( r \sim \beta_{\mu_1}(R_q^k), e_1, e_2 \sim \beta_{\mu_2}(R_q) \) |
| 🔹 **Calcula los componentes cifrados:** | |
| 🔹 \( u = A^T r + e_1 \)  | Primera parte del cifrado |
| 🔹 \( v = b^T r + e_2 + K \) | Segunda parte del cifrado |
| 🔹 **Envía el mensaje cifrado** \( c = (u, v) \) a Bob. | 🔒 |

🔒 **Seguridad MLWE:** \( u \) y \( v \) están protegidos por el ruido, haciendo difícil recuperar \( K \) sin \( s \).

---

## 🔓 Paso 3: Bob Descifra la Clave (Decaps - Basado en MLWE)  
Bob usa su clave secreta \( s \) para recuperar \( K \).  

| **Bob (Receptor)** | **Acción** |
|--------------------|------------|
| 🔹 **Descompone \( c = (u, v) \)** para obtener \( u \) y \( v \). | |
| 🔹 **Calcula:** \( K = v - s^T u \). | 🔑 |
| 🔹 **Recupera \( K \) con un pequeño error** (pero sigue siendo utilizable). | ✅ |

---

## 🔄 Resumen de la Relación con MLWE  
- En **KeyGen**, Bob usa MLWE para generar una clave pública difícil de invertir.  
- En **Encaps**, Alice usa la clave pública para cifrar \( K \) con MLWE.  
- En **Decaps**, Bob usa su clave privada \( s \) para recuperar \( K \).  

✅ **Kyber-KEM usa MLWE en PKE y lo extiende para encapsular claves de sesión seguras.**  
