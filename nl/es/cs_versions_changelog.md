---

copyright:
  years: 2014, 2018
lastupdated: "2018-10-25"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:pre: .pre}
{:table: .aria-labeledby="caption"}
{:codeblock: .codeblock}
{:tip: .tip}
{:download: .download}



# Registro de cambios de versiones
{: #changelog}

Visualice información de cambios de versiones de actualizaciones mayores, menores y parches de actualización que están disponibles para los clústeres {{site.data.keyword.containerlong}} Kubernetes. Los cambios incluyen actualizaciones a Kubernetes y a los componentes de Proveedores de {{site.data.keyword.Bluemix_notm}}.
{:shortdesc}

Para obtener más información acerca de las versiones principales, secundarias y de parche y sobre las acciones de migración entre versiones menores, consulte [Versiones de Kubernetes](cs_versions.html).
{: tip}

Para obtener información sobre los cambios desde la versión anterior, consulte los siguientes registros de cambios.
-  [Registros de cambios](#111_changelog) de la versión 1.11.
-  [Registros de cambios](#110_changelog) de la versión 1.10.
-  [Registros de cambios](#19_changelog) de la versión 1.9.
-  [Archivo](#changelog_archive) de registros de cambios para versiones no soportadas o en desuso.

**Nota**: algunos registros de cambios son para _fixpacks de nodos trabajadores_ y solo se aplican a los nodos trabajadores. Debe [aplicar estos parches](cs_cli_reference.html#cs_worker_update) para garantizar la conformidad de seguridad de los nodos trabajadores. Otros registros de cambios son para _fixpacks de nodo maestro_ y solo se aplican al nodo maestro del clúster. Es posible que los fixpacks de nodo maestro no se apliquen automáticamente. Puede optar por [aplicarlos manualmente](cs_cli_reference.html#cs_cluster_update). Para obtener más información sobre los tipos de parches, consulte [Tipos de actualizaciones](cs_versions.html#update_types).

</br>

## Registro de cambios de la versión 1.11
{: #111_changelog}

Revise los siguientes cambios.


### Registro de cambios para fixpack de nodo maestro 1.11.3_1527, publicado el 15 de octubre de 2018
{: #1113_1527}

<table summary="Cambios realizados desde la versión 1.11.3_1524">
<caption>Cambios desde la versión 1.11.3_1524</caption>
<thead>
<tr>
<th>Componente</th>
<th>Anterior</th>
<th>Actual</th>
<th>Descripción</th>
</tr>
</thead>
<tbody>
<tr>
<td>Configuración de Calico</td>
<td>N/D</td>
<td>N/D</td>
<td>Se ha corregido el analizador de preparación del contenedor `calico-node` para manejar mejor las anomalías de nodo.</td>
</tr>
<tr>
<td>Actualización de clúster</td>
<td>N/D</td>
<td>N/D</td>
<td>Se ha corregido el problema con la actualización de los complementos de clúster cuando el nodo maestro se actualiza desde una versión no soportada.</td>
</tr>
</tbody>
</table>

### Registro de cambios para el fix pack de nodo trabajador 1.11.3_1525, publicado el 10 de octubre de 2018
{: #1113_1525}

<table summary="Cambios realizados desde la versión 1.11.3_1524">
<caption>Cambios desde la versión 1.11.3_1524</caption>
<thead>
<tr>
<th>Componente</th>
<th>Anterior</th>
<th>Actual</th>
<th>Descripción</th>
</tr>
</thead>
<tbody>
<tr>
<td>Kernel</td>
<td>4.4.0-133</td>
<td>4.4.0-137</td>
<td>Se han actualizado las imágenes de nodo trabajador con la actualización de kernel para [CVE-2018-14633, CVE-2018-17182 ![Icono de enlace externo](../icons/launch-glyph.svg "Icono de enlace externo")](https://changelogs.ubuntu.com/changelogs/pool/main/l/linux/linux_4.4.0-137.163/changelog).</td>
</tr>
<tr>
<td>Tiempo de espera de sesión inactiva</td>
<td>N/D</td>
<td>N/D</td>
<td>Establezca el tiempo de espera de sesión inactiva en 5 minutos por razones de conformidad.</td>
</tr>
</tbody>
</table>


### Registro de cambios para 1.11.3_1524, publicado el 2 de octubre de 2018
{: #1113_1524}

<table summary="Cambios realizados desde la versión 1.11.3_1521">
<caption>Cambios desde la versión 1.11.3_1521</caption>
<thead>
<tr>
<th>Componente</th>
<th>Anterior</th>
<th>Actual</th>
<th>Descripción</th>
</tr>
</thead>
<tbody>
<tr>
<td>containerd</td>
<td>1.1.3</td>
<td>1.1.4</td>
<td>Consulte las [notas del release de containerd ![Icono de enlace externo](../icons/launch-glyph.svg "Icono de enlace externo")](https://github.com/containerd/containerd/releases/tag/v1.1.4).</td>
</tr>
<tr>
<td>Proveedor de {{site.data.keyword.Bluemix_notm}}</td>
<td>v1.11.3-91</td>
<td>v1.11.3-100</td>
<td>Se ha actualizado el enlace de la documentación en los mensajes de error del equilibrador de carga.</td>
</tr>
<tr>
<td>Clases de almacenamiento de archivos de IBM</td>
<td>N/D</td>
<td>N/D</td>
<td>Se ha eliminado el parámetro `reclaimPolicy` duplicado de las clases de almacenamiento de archivos de IBM.<br><br>
Además, ahora, cuando actualiza el nodo maestro del clúster, la clase de almacenamiento de archivos predeterminada de IBM no se modifica. Si desea cambiar la clase de almacenamiento predeterminada, ejecute el mandato `kubectl parche storageclass <storageclass> -p '{"metadata": {"annotations":{"storageclass.kubernetes.io/is-default-class":"true"}}}'` y sustituya `<storageclass>` por el nombre de la clase de almacenamiento.</td>
</tr>
</tbody>
</table>

### Registro de cambios para 1.11.3_1521, publicado el 20 de septiembre de 2018
{: #1113_1521}

<table summary="Cambios realizados desde la versión 1.11.2_1516">
<caption>Cambios desde la versión 1.11.2_1516</caption>
<thead>
<tr>
<th>Componente</th>
<th>Anterior</th>
<th>Actual</th>
<th>Descripción</th>
</tr>
</thead>
<tbody>
<tr>
<td>Proveedor de {{site.data.keyword.Bluemix_notm}}</td>
<td>v1.11.2-71</td>
<td>v1.11.3-91</td>
<td>Actualizado para dar soporte al release 1.11.3 de Kubernetes.</td>
</tr>
<tr>
<td>Clases de almacenamiento de archivos de IBM</td>
<td>N/D</td>
<td>N/D</td>
<td>Se ha eliminado `mountOptions` en las clases de almacenamiento de archivos de IBM para utilizar el valor predeterminado que proporciona el nodo trabajador.<br><br>
Además, ahora, cuando actualiza el nodo maestro del clúster, la clase de almacenamiento de archivos predeterminada de IBM sigue siendo `ibmc-file-bronze`. Si desea cambiar la clase de almacenamiento predeterminada, ejecute el mandato `kubectl parche storageclass <storageclass> -p '{"metadata": {"annotations":{"storageclass.kubernetes.io/is-default-class":"true"}}}'` y sustituya `<storageclass>` por el nombre de la clase de almacenamiento.</td>
</tr>
<tr>
<td>Proveedor de servicios de gestión de claves</td>
<td>N/D</td>
<td>N/D</td>
<td>Se ha añadido la capacidad de utilizar el proveedor Kubernetes de servicio de gestión de claves (KMS) en el clúster, para dar soporte a {{site.data.keyword.keymanagementservicefull}}. Cuando se [habilita {{site.data.keyword.keymanagementserviceshort}} en el clúster](cs_encrypt.html#keyprotect), todos los secretos de Kubernetes se cifran.</td>
</tr>
<tr>
<td>Kubernetes</td>
<td>v1.11.2</td>
<td>v1.11.3</td>
<td>Consulte las [notas del release de Kubernetes ![Icono de enlace externo](../icons/launch-glyph.svg "Icono de enlace externo")](https://github.com/kubernetes/kubernetes/releases/tag/v1.11.3).</td>
</tr>
<tr>
<td>Kubernetes DNS Autoscaler</td>
<td>1.1.2-r2</td>
<td>1.2.0</td>
<td>Consulte las [notas del release de Kubernetes DNS Autoscaler ![Icono de enlace externo](../icons/launch-glyph.svg "Icono de enlace externo")](https://github.com/kubernetes-incubator/cluster-proportional-autoscaler/releases/tag/1.2.0).</td>
</tr>
<tr>
<td>Rotación de registros</td>
<td>N/D</td>
<td>N/D</td>
<td>Se ha modificado para utilizar temporizadores `systemd` en lugar de `cronjobs` para evitar que `logrotate` falle en los nodos trabajadores que no se han vuelto a cargar o no se han actualizado en 90 días. **Nota**: en
todas las versiones anteriores de este release menor, el disco primario se llenaba después de que fallar el trabajo cron porque los registros no se rotaban. El trabajo cron falla después de que el nodo trabajador esté activo durante 90 días sin que se haya actualizado o recargado. Si los registros llenan todo el disco primario, el nodo trabajador entra en un estado de error. El nodo trabajador se puede arreglar mediante el [mandato](cs_cli_reference.html#cs_worker_reload) `ibmcloud ks worker-reload` o el [mandato](cs_cli_reference.html#cs_worker_update) `ibmcloud ks worker-update`.</td>
</tr>
<tr>
<td>Caducidad de la contraseña raíz</td>
<td>N/D</td>
<td>N/D</td>
<td>Las contraseñas raíz para los nodos trabajadores caducan después de 90 días por razones de conformidad. Si las herramientas de automatización tienen que iniciar la sesión en el nodo trabajador como usuario root o se basan en trabajos cron que se ejecutan como root, puede inhabilitar la caducidad de la contraseña iniciando una sesión en el nodo de trabajo y ejecutando `chage -M -1 root`. **Nota**: si tiene requisitos de conformidad de seguridad que impiden la ejecución como root o la eliminación de la caducidad de la contraseña, no inhabilite la caducidad. En lugar de ello, puede [actualizar](cs_cli_reference.html#cs_worker_update) o [volver a cargar](cs_cli_reference.html#cs_worker_reload) los nodos trabajadores al menos cada 90 días.</td>
</tr>
<tr>
<td>Componentes de tiempo de ejecución de nodo trabajador (`kubelet`, `kube-proxy`, `containerd`)</td>
<td>N/D</td>
<td>N/D</td>
<td>Se han eliminado las dependencias de los componentes de tiempo de ejecución en el disco primario. Esta mejora impide que los nodos trabajadores fallen cuando se llena el disco primario.</td>
</tr>
<tr>
<td>Systemd</td>
<td>N/D</td>
<td>N/D</td>
<td>Limpie de forma periódica las unidades de montaje transitorias para evitar que se desborden. Esta acción está relacionada con el [problema de Kubernetes 57345 ![Icono de enlace externo](../icons/launch-glyph.svg "Icono de enlace externo")](https://github.com/kubernetes/kubernetes/issues/57345).</td>
</tr>
</tbody>
</table>

### Registro de cambios para 1.11.2_1516, publicado el 4 de septiembre de 2018
{: #1112_1516}

<table summary="Cambios realizados desde la versión 1.11.2_1514">
<caption>Cambios desde la versión 1.11.2_1514</caption>
<thead>
<tr>
<th>Componente</th>
<th>Anterior</th>
<th>Actual</th>
<th>Descripción</th>
</tr>
</thead>
<tbody>
<tr>
<td>Calico</td>
<td>v3.1.3</td>
<td>v3.2.1</td>
<td>Consulte las [notas del release de Calico ![Icono de enlace externo](../icons/launch-glyph.svg "Icono de enlace externo")](https://docs.projectcalico.org/v3.2/releases/#v321).</td>
</tr>
<tr>
<td>containerd</td>
<td>1.1.2</td>
<td>1.1.3</td>
<td>Consulte las [notas del release de `containerd` ![Icono de enlace externo](../icons/launch-glyph.svg "Icono de enlace externo")](https://github.com/containerd/containerd/releases/tag/v1.1.3).</td>
</tr>
<tr>
<td>Proveedor de {{site.data.keyword.Bluemix_notm}}</td>
<td>v1.11.2-60</td>
<td>v1.11.2-71</td>
<td>Se ha cambiado la configuración del proveedor de nube para manejar mejor las actualizaciones para los servicios de equilibrador de carga con `externalTrafficPolicy` establecido en `local`.</td>
</tr>
<tr>
<td>Configuración del plugin de almacenamiento de archivos de IBM</td>
<td>N/D</td>
<td>N/D</td>
<td>Se ha eliminado la versión de NFS predeterminada de las opciones de montaje de las clases de almacenamiento de archivos proporcionadas por IBM. El sistema operativo del host ahora negocia la versión de NFS con el servidor NFS de la infraestructura de IBM Cloud (SoftLayer). Para establecer manualmente una versión de NFS específica, o para cambiar la versión de NFS de su PV que ha sido negociada por el sistema operativo del host, consulte [Cambio de la versión predeterminada de NFS](cs_storage_file.html#nfs_version_class).</td>
</tr>
</tbody>
</table>

### Registro de cambios para el fix pack de nodo trabajador 1.11.2_1514, publicado el 23 de agosto de 2018
{: #1112_1514}

<table summary="Cambios realizados desde la versión 1.11.2_1513">
<caption>Cambios desde la versión 1.11.2_1513</caption>
<thead>
<tr>
<th>Componente</th>
<th>Anterior</th>
<th>Actual</th>
<th>Descripción</th>
</tr>
</thead>
<tbody>
<tr>
<td>`systemd`</td>
<td>229</td>
<td>230</td>
<td>Se ha actualizado `systemd` para arreglar la fuga de `cgroup`.</td>
</tr>
<tr>
<td>Kernel</td>
<td>4.4.0-127</td>
<td>4.4.0-133</td>
<td>Se han actualizado las imágenes de nodo trabajador con la actualización de kernel para [CVE-2018-3620, CVE-2018-3646 ![Icono de enlace externo](../icons/launch-glyph.svg "Icono de enlace externo")](https://usn.ubuntu.com/3741-1/).</td>
</tr>
</tbody>
</table>

### Registro de cambios para 1.11.2_1513, publicado el 14 de agosto de 2018
{: #1112_1513}

<table summary="Cambios realizados desde la versión 1.10.5_1518">
<caption>Cambios desde la versión 1.10.5_1518</caption>
<thead>
<tr>
<th>Componente</th>
<th>Anterior</th>
<th>Actual</th>
<th>Descripción</th>
</tr>
</thead>
<tbody>
<tr>
<td>containerd</td>
<td>N/D</td>
<td>1.1.2</td>
<td>`containerd` sustituye a Docker como el nuevo tiempo de ejecución de contenedor para Kubernetes. Consulte las [notas del release de `containerd` ![Icono de enlace externo](../icons/launch-glyph.svg "Icono de enlace externo")](https://github.com/containerd/containerd/releases/tag/v1.1.2). Para conocer las acciones que debe llevar a cabo, consulte [Migración a `containerd` como tiempo de ejecución de contenedor](cs_versions.html#containerd).</td>
</tr>
<tr>
<td>Docker</td>
<td>N/D</td>
<td>N/D</td>
<td>`containerd` sustituye a Docker como el nuevo tiempo de ejecución de contenedor para Kubernetes, para mejorar el rendimiento. Para conocer las acciones que debe llevar a cabo, consulte [Migración a `containerd` como tiempo de ejecución de contenedor](cs_versions.html#containerd).</td>
</tr>
<tr>
<td>etcd</td>
<td>v3.2.14</td>
<td>v3.2.18</td>
<td>Consulte las [notas del release de etcd ![Icono de enlace externo](../icons/launch-glyph.svg "Icono de enlace externo")](https://github.com/coreos/etcd/releases/v3.2.18).</td>
</tr>
<tr>
<td>Proveedor de {{site.data.keyword.Bluemix_notm}}</td>
<td>v1.10.5-118</td>
<td>v1.11.2-60</td>
<td>Actualizado para dar soporte al release 1.11 de Kubernetes. Además, los pods de equilibrador de carga ahora utilizan la nueva clase de prioridad de pod `ibm-app-cluster-critical`.</td>
</tr>
<tr>
<td>Plugin de almacenamiento de archivos de IBM</td>
<td>334</td>
<td>338</td>
<td>Se ha actualizado la versión de `incubator` a 1.8. El almacenamiento de archivos se suministra a la zona específica que seleccione. No puede actualizar las etiquetas de instancia de PV existentes (estáticas) a menos que esté utilizando un clúster multizona y tenga que [añadir las etiquetas de zona y de región](cs_storage_basics.html#multizone).</td>
</tr>
<tr>
<td>Kubernetes</td>
<td>v1.10.5</td>
<td>v1.11.2</td>
<td>Consulte las [notas del release de Kubernetes ![Icono de enlace externo](../icons/launch-glyph.svg "Icono de enlace externo")](https://github.com/kubernetes/kubernetes/releases/tag/v1.11.2).</td>
</tr>
<tr>
<td>Configuración de Kubernetes</td>
<td>N/D</td>
<td>N/D</td>
<td>Se ha actualizado la configuración de OpenID Connect para el servidor de API de Kubernetes del clúster para dar soporte a los grupos de acceso de {{site.data.keyword.Bluemix_notm}} Identity Access and Management (IAM). Se ha añadido `Priority` a la opción `--enable-admission-plugins` para el servidor de API de Kubernetes del clúster y se ha configurado el clúster para que dé soporte a la prioridad de pod. Para obtener más información, consulte:
<ul><li>[Grupos de acceso de IAM](cs_users.html#rbac)</li>
<li>[Configuración de la prioridad de pod](cs_pod_priority.html#pod_priority)</li></ul></td>
</tr>
<tr>
<td>Kubernetes Heapster</td>
<td>v1.5.2</td>
<td>v.1.5.4</td>
<td>Se han aumentado los límites de recursos para el contenedor `heapster-nanny`. Consulte las notas del release de [Kubernetes Heapster ![Icono de enlace externo](../icons/launch-glyph.svg "Icono de enlace externo")](https://github.com/kubernetes/heapster/releases/tag/v1.5.4).</td>
</tr>
<tr>
<td>Configuración de registro</td>
<td>N/D</td>
<td>N/D</td>
<td>El directorio de registro de contenedor ahora es `/var/log/pods/` en lugar del valor anterior `/var/lib/docker/containers/`.</td>
</tr>
</tbody>
</table>

<br />


## Registro de cambios de la versión 1.10
{: #110_changelog}

Revise los siguientes cambios.

### Registro de cambios para fixpack de nodo maestro 1.10.8_1527, publicado el 15 de octubre de 2018
{: #1108_1527}

<table summary="Resumen de cambios realizados desde la versión 1.10.8_1524">
<caption>Cambios desde la versión 1.10.8_1524</caption>
<thead>
<tr>
<th>Componente</th>
<th>Anterior</th>
<th>Actual</th>
<th>Descripción</th>
</tr>
</thead>
<tbody>
<tr>
<td>Configuración de Calico</td>
<td>N/D</td>
<td>N/D</td>
<td>Se ha corregido el analizador de preparación del contenedor `calico-node` para manejar mejor las anomalías de nodo.</td>
</tr>
<tr>
<td>Actualización de clúster</td>
<td>N/D</td>
<td>N/D</td>
<td>Se ha corregido el problema con la actualización de los complementos de clúster cuando el nodo maestro se actualiza desde una versión no soportada.</td>
</tr>
</tbody>
</table>

### Registro de cambios para el fix pack de nodo trabajador 1.10.8_1525, publicado el 10 de octubre de 2018
{: #1108_1525}

<table summary="Resumen de cambios realizados desde la versión 1.10.8_1524">
<caption>Cambios desde la versión 1.10.8_1524</caption>
<thead>
<tr>
<th>Componente</th>
<th>Anterior</th>
<th>Actual</th>
<th>Descripción</th>
</tr>
</thead>
<tbody>
<tr>
<td>Kernel</td>
<td>4.4.0-133</td>
<td>4.4.0-137</td>
<td>Se han actualizado las imágenes de nodo trabajador con la actualización de kernel para [CVE-2018-14633, CVE-2018-17182 ![Icono de enlace externo](../icons/launch-glyph.svg "Icono de enlace externo")](https://changelogs.ubuntu.com/changelogs/pool/main/l/linux/linux_4.4.0-137.163/changelog).</td>
</tr>
<tr>
<td>Tiempo de espera de sesión inactiva</td>
<td>N/D</td>
<td>N/D</td>
<td>Establezca el tiempo de espera de sesión inactiva en 5 minutos por razones de conformidad.</td>
</tr>
</tbody>
</table>


### Registro de cambios para 1.10.8_1524, publicado el 2 de octubre de 2018
{: #1108_1524}

<table summary="Cambios realizados desde la versión 1.10.7_1520">
<caption>Cambios desde la versión 1.10.7_1520</caption>
<thead>
<tr>
<th>Componente</th>
<th>Anterior</th>
<th>Actual</th>
<th>Descripción</th>
</tr>
</thead>
<tbody>
<tr>
<td>Proveedor de servicios de gestión de claves</td>
<td>N/D</td>
<td>N/D</td>
<td>Se ha añadido la capacidad de utilizar el proveedor Kubernetes de servicio de gestión de claves (KMS) en el clúster, para dar soporte a {{site.data.keyword.keymanagementservicefull}}. Cuando se [habilita {{site.data.keyword.keymanagementserviceshort}} en el clúster](cs_encrypt.html#keyprotect), todos los secretos de Kubernetes se cifran.</td>
</tr>
<tr>
<td>Kubernetes</td>
<td>v1.10.7</td>
<td>v1.10.8</td>
<td>Consulte las [notas del release de Kubernetes ![Icono de enlace externo](../icons/launch-glyph.svg "Icono de enlace externo")](https://github.com/kubernetes/kubernetes/releases/tag/v1.10.8).</td>
</tr>
<tr>
<td>Kubernetes DNS Autoscaler</td>
<td>1.1.2-r2</td>
<td>1.2.0</td>
<td>Consulte las [notas del release de Kubernetes DNS Autoscaler ![Icono de enlace externo](../icons/launch-glyph.svg "Icono de enlace externo")](https://github.com/kubernetes-incubator/cluster-proportional-autoscaler/releases/tag/1.2.0).</td>
</tr>
<tr>
<td>Proveedor de {{site.data.keyword.Bluemix_notm}}</td>
<td>v1.10.7-146</td>
<td>v1.10.8-172</td>
<td>Actualizado para dar soporte al release 1.10.8 de Kubernetes. También se ha actualizado el enlace de la documentación en los mensajes de error del equilibrador de carga.</td>
</tr>
<tr>
<td>Clases de almacenamiento de archivos de IBM</td>
<td>N/D</td>
<td>N/D</td>
<td>Se ha eliminado `mountOptions` en las clases de almacenamiento de archivos de IBM para utilizar el valor predeterminado que proporciona el nodo trabajador. Se ha eliminado el parámetro `reclaimPolicy` duplicado de las clases de almacenamiento de archivos de IBM.<br><br>
Además, ahora, cuando actualiza el nodo maestro del clúster, la clase de almacenamiento de archivos predeterminada de IBM no se modifica. Si desea cambiar la clase de almacenamiento predeterminada, ejecute el mandato `kubectl parche storageclass <storageclass> -p '{"metadata": {"annotations":{"storageclass.kubernetes.io/is-default-class":"true"}}}'` y sustituya `<storageclass>` por el nombre de la clase de almacenamiento.</td>
</tr>
</tbody>
</table>

### Registro de cambios para el fix pack de nodo trabajador 1.10.7_1521, publicado el 20 de septiembre de 2018
{: #1107_1521}

<table summary="Cambios realizados desde la versión 1.10.7_1520">
<caption>Cambios desde la versión 1.10.7_1520</caption>
<thead>
<tr>
<th>Componente</th>
<th>Anterior</th>
<th>Actual</th>
<th>Descripción</th>
</tr>
</thead>
<tbody>
<tr>
<td>Rotación de registros</td>
<td>N/D</td>
<td>N/D</td>
<td>Se ha modificado para utilizar temporizadores `systemd` en lugar de `cronjobs` para evitar que `logrotate` falle en los nodos trabajadores que no se han vuelto a cargar o no se han actualizado en 90 días. **Nota**: en
todas las versiones anteriores de este release menor, el disco primario se llenaba después de que fallar el trabajo cron porque los registros no se rotaban. El trabajo cron falla después de que el nodo trabajador esté activo durante 90 días sin que se haya actualizado o recargado. Si los registros llenan todo el disco primario, el nodo trabajador entra en un estado de error. El nodo trabajador se puede arreglar mediante el [mandato](cs_cli_reference.html#cs_worker_reload) `ibmcloud ks worker-reload` o el [mandato](cs_cli_reference.html#cs_worker_update) `ibmcloud ks worker-update`.</td>
</tr>
<tr>
<td>Componentes de tiempo de ejecución de nodo trabajador (`kubelet`, `kube-proxy`, `docker`)</td>
<td>N/D</td>
<td>N/D</td>
<td>Se han eliminado las dependencias de los componentes de tiempo de ejecución en el disco primario. Esta mejora impide que los nodos trabajadores fallen cuando se llena el disco primario.</td>
</tr>
<tr>
<td>Caducidad de la contraseña raíz</td>
<td>N/D</td>
<td>N/D</td>
<td>Las contraseñas raíz para los nodos trabajadores caducan después de 90 días por razones de conformidad. Si las herramientas de automatización tienen que iniciar la sesión en el nodo trabajador como usuario root o se basan en trabajos cron que se ejecutan como root, puede inhabilitar la caducidad de la contraseña iniciando una sesión en el nodo de trabajo y ejecutando `chage -M -1 root`. **Nota**: si tiene requisitos de conformidad de seguridad que impiden la ejecución como root o la eliminación de la caducidad de la contraseña, no inhabilite la caducidad. En lugar de ello, puede [actualizar](cs_cli_reference.html#cs_worker_update) o [volver a cargar](cs_cli_reference.html#cs_worker_reload) los nodos trabajadores al menos cada 90 días.</td>
</tr>
<tr>
<td>Systemd</td>
<td>N/D</td>
<td>N/D</td>
<td>Limpie de forma periódica las unidades de montaje transitorias para evitar que se desborden. Esta acción está relacionada con el [problema de Kubernetes 57345 ![Icono de enlace externo](../icons/launch-glyph.svg "Icono de enlace externo")](https://github.com/kubernetes/kubernetes/issues/57345).</td>
</tr>
<tr>
<td>Docker</td>
<td>N/D</td>
<td>N/D</td>
<td>Inhabilite el puente de Docker predeterminado para que se utilice el rango de IP `172.17.0.0/16` para las rutas privadas. Si crea los contenedores Docker en los nodos trabajadores ejecutando los mandatos `docker` en el host directamente o utilizando un pod que monta el socket de Docker, elija una de las opciones siguientes.<ul><li>Para garantizar la conectividad de red externa al crear el contenedor, ejecute `docker build . --network host`.</li>
<li>Para crear de forma explícita una red para utilizarla al crear el contenedor, ejecute `docker network create` y luego utilice esta red.</li></ul>
**Nota**: ¿Tiene dependencias en el socket Docker o Docker directamente? [Mire a `containerd` en lugar de a `docker` como entorno de ejecución del contenedor](cs_versions.html#containerd) para que los clústeres estén preparados para ejecutar Kubernetes versión 1.11 o posteriores.</td>
</tr>
</tbody>
</table>

### Registro de cambios para 1.10.7_1520, publicado el 4 de septiembre de 2018
{: #1107_1520}

<table summary="Cambios realizados desde la versión 1.10.5_1519">
<caption>Cambios desde la versión 1.10.5_1519</caption>
<thead>
<tr>
<th>Componente</th>
<th>Anterior</th>
<th>Actual</th>
<th>Descripción</th>
</tr>
</thead>
<tbody>
<tr>
<td>Calico</td>
<td>v3.1.3</td>
<td>v3.2.1</td>
<td>Consulte las [notas del release de Calico ![Icono de enlace externo](../icons/launch-glyph.svg "Icono de enlace externo")](https://docs.projectcalico.org/v3.2/releases/#v321).</td>
</tr>
<tr>
<td>Proveedor de {{site.data.keyword.Bluemix_notm}}</td>
<td>v1.10.5-118</td>
<td>v1.10.7-146</td>
<td>Actualizado para dar soporte al release 1.10.7 de Kubernetes. Además, se ha cambiado la configuración del proveedor de nube para manejar mejor las actualizaciones para los servicios de equilibrador de carga con `externalTrafficPolicy` establecido en `local`.</td>
</tr>
<tr>
<td>Plugin de almacenamiento de archivos de IBM</td>
<td>334</td>
<td>338</td>
<td>Se ha actualizado la versión de incubator a 1.8. El almacenamiento de archivos se suministra a la zona específica que seleccione. No puede actualizar las etiquetas de una instancia de PV existente (estática) a menos que esté utilizando un clúster multizona y tenga que añadir las etiquetas de zona y de región.<br><br> Se ha eliminado la versión de NFS predeterminada de las opciones de montaje de las clases de almacenamiento de archivos proporcionadas por IBM. El sistema operativo del host ahora negocia la versión de NFS con el servidor NFS de la infraestructura de IBM Cloud (SoftLayer). Para establecer manualmente una versión de NFS específica, o para cambiar la versión de NFS de su PV que ha sido negociada por el sistema operativo del host, consulte [Cambio de la versión predeterminada de NFS](cs_storage_file.html#nfs_version_class).</td>
</tr>
<tr>
<td>Kubernetes</td>
<td>v1.10.5</td>
<td>v1.10.7</td>
<td>Consulte las [notas del release de Kubernetes ![Icono de enlace externo](../icons/launch-glyph.svg "Icono de enlace externo")](https://github.com/kubernetes/kubernetes/releases/tag/v1.10.7).</td>
</tr>
<tr>
<td>Configuración de Kubernetes Heapster</td>
<td>N/D</td>
<td>N/D</td>
<td>Se han aumentado los límites de recursos para el contenedor `heapster-nanny`.</td>
</tr>
</tbody>
</table>

### Registro de cambios para el fix pack de nodo trabajador 1.10.5_1519, publicado el 23 de agosto de 2018
{: #1105_1519}

<table summary="Cambios realizados desde la versión 1.10.5_1518">
<caption>Cambios desde la versión 1.10.5_1518</caption>
<thead>
<tr>
<th>Componente</th>
<th>Anterior</th>
<th>Actual</th>
<th>Descripción</th>
</tr>
</thead>
<tbody>
<tr>
<td>`systemd`</td>
<td>229</td>
<td>230</td>
<td>Se ha actualizado `systemd` para arreglar la fuga de `cgroup`.</td>
</tr>
<tr>
<td>Kernel</td>
<td>4.4.0-127</td>
<td>4.4.0-133</td>
<td>Se han actualizado las imágenes de nodo trabajador con la actualización de kernel para [CVE-2018-3620, CVE-2018-3646 ![Icono de enlace externo](../icons/launch-glyph.svg "Icono de enlace externo")](https://usn.ubuntu.com/3741-1/).</td>
</tr>
</tbody>
</table>


### Registro de cambios para el fix pack de nodo trabajador 1.10.5_1518, publicado el 13 de agosto de 2018
{: #1105_1518}

<table summary="Cambios realizados desde la versión 1.10.5_1517">
<caption>Cambios desde la versión 1.10.5_1517</caption>
<thead>
<tr>
<th>Componente</th>
<th>Anterior</th>
<th>Actual</th>
<th>Descripción</th>
</tr>
</thead>
<tbody>
<tr>
<td>Paquetes Ubuntu</td>
<td>N/D</td>
<td>N/D</td>
<td>Actualizaciones de los paquetes de Ubuntu instalados.</td>
</tr>
</tbody>
</table>

### Registro de cambios para 1.10.5_1517, publicado el 27 de julio de 2018
{: #1105_1517}

<table summary="Cambios realizados desde la versión 1.10.3_1514">
<caption>Cambios desde la versión 1.10.3_1514</caption>
<thead>
<tr>
<th>Componente</th>
<th>Anterior</th>
<th>Actual</th>
<th>Descripción</th>
</tr>
</thead>
<tbody>
<tr>
<td>Calico</td>
<td>v3.1.1</td>
<td>v3.1.3</td>
<td>Consulte las [notas del release de Calico ![Icono de enlace externo](../icons/launch-glyph.svg "Icono de enlace externo")](https://docs.projectcalico.org/v3.1/releases/#v313).</td>
</tr>
<tr>
<td>Proveedor de {{site.data.keyword.Bluemix_notm}}</td>
<td>v1.10.3-85</td>
<td>v1.10.5-118</td>
<td>Actualizado para dar soporte al release 1.10.5 de Kubernetes. Además, ahora los sucesos del servicio de LoadBalancer `create failure` incluyen cualquier error de subred portátil.</td>
</tr>
<tr>
<td>Plugin de almacenamiento de archivos de IBM</td>
<td>320</td>
<td>334</td>
<td>Se ha aumentado el tiempo de espera para la creación de un volumen persistente de 15 a 30 minutos. Se ha cambiado el tipo de facturación predeterminado a `por hora`. Se han añadido opciones de montaje a las clases de almacenamiento predefinidas. En la instancia de almacenamiento de archivos NFS de la cuenta de infraestructura de IBM Cloud (SoftLayer), se ha cambiado el campo **Notas** por el formato JSON y se ha añadido el espacio de nombres de Kubernetes en el que se ha desplegado el PV. Para dar soporte a clústeres multizona, se han añadido etiquetas de zona y región a los volúmenes persistentes.</td>
</tr>
<tr>
<td>Kubernetes</td>
<td>v1.10.3</td>
<td>v1.10.5</td>
<td>Consulte las [notas del release de Kubernetes ![Icono de enlace externo](../icons/launch-glyph.svg "Icono de enlace externo")](https://github.com/kubernetes/kubernetes/releases/tag/v1.10.5).</td>
</tr>
<tr>
<td>Kernel</td>
<td>N/D</td>
<td>N/D</td>
<td>Mejoras menores en los valores de red del nodo trabajador para las cargas de trabajo de red de alto rendimiento.</td>
</tr>
<tr>
<td>Cliente OpenVPN</td>
<td>N/D</td>
<td>N/D</td>
<td>El despliegue de cliente de OpenVPN `vpn` que se ejecuta en el espacio de nombres `kube-system` ahora se gestiona mediante `addon-manager` de Kubernetes.</td>
</tr>
</tbody>
</table>

### Registro de cambios para el fix pack de nodo trabajador 1.10.3_1514, publicado el 3 de julio de 2018
{: #1103_1514}

<table summary="Cambios realizados desde la versión 1.10.3_1513">
<caption>Cambios desde la versión 1.10.3_1513</caption>
<thead>
<tr>
<th>Componente</th>
<th>Anterior</th>
<th>Actual</th>
<th>Descripción</th>
</tr>
</thead>
<tbody>
<tr>
<td>Kernel</td>
<td>N/D</td>
<td>N/D</td>
<td>Se ha optimizado `sysctl` para las cargas de trabajo de red de alto rendimiento.</td>
</tr>
</tbody>
</table>


### Registro de cambios para el fix pack de nodo trabajador 1.10.3_1513, publicado el 21 de junio de 2018
{: #1103_1513}

<table summary="Cambios realizados desde la versión 1.10.3_1512">
<caption>Cambios desde la versión 1.10.3_1512</caption>
<thead>
<tr>
<th>Componente</th>
<th>Anterior</th>
<th>Actual</th>
<th>Descripción</th>
</tr>
</thead>
<tbody>
<tr>
<td>Docker</td>
<td>N/D</td>
<td>N/D</td>
<td>Para los tipos de máquina no cifrados, el disco secundario se limpia obteniendo un sistema de archivos nuevo cuando se vuelve a cargar o se actualiza el nodo trabajador.</td>
</tr>
</tbody>
</table>

### Registro de cambios para 1.10.3_1512, publicado el 12 de junio de 2018
{: #1103_1512}

<table summary="Cambios realizados desde la versión 1.10.1_1510">
<caption>Cambios desde la versión 1.10.1_1510</caption>
<thead>
<tr>
<th>Componente</th>
<th>Anterior</th>
<th>Actual</th>
<th>Descripción</th>
</tr>
</thead>
<tbody>
<tr>
<td>Kubernetes</td>
<td>v1.10.1</td>
<td>v1.10.3</td>
<td>Consulte las [notas del release de Kubernetes ![Icono de enlace externo](../icons/launch-glyph.svg "Icono de enlace externo")](https://github.com/kubernetes/kubernetes/releases/tag/v1.10.3).</td>
</tr>
<tr>
<td>Configuración de Kubernetes</td>
<td>N/D</td>
<td>N/D</td>
<td>Se ha añadido `PodSecurityPolicy` a la opción `--enable-admission-plugins` para el servidor de API de Kubernetes del clúster y se ha configurado el clúster para que dé soporte a las políticas de seguridad de pod. Para obtener más información, consulte [Configuración de políticas de seguridad de pod](cs_psp.html).</td>
</tr>
<tr>
<td>Configuración de Kubelet</td>
<td>N/D</td>
<td>N/D</td>
<td>Se ha habilitado la opción `--authentication-token-webhook` para dar soporte a las señales de portadora de API y de cuenta de servicio para la autenticación ante el punto final HTTPS de `kubelet`.</td>
</tr>
<tr>
<td>Proveedor de {{site.data.keyword.Bluemix_notm}}</td>
<td>v1.10.1-52</td>
<td>v1.10.3-85</td>
<td>Actualizado para dar soporte al release 1.10.3 de Kubernetes.</td>
</tr>
<tr>
<td>Cliente OpenVPN</td>
<td>N/D</td>
<td>N/D</td>
<td>Se ha añadido `livenessProbe` al despliegue de cliente de OpenVPN `vpn` que se ejecuta en el espacio de nombres `kube-system`.</td>
</tr>
<tr>
<td>Actualización del kernel</td>
<td>4.4.0-116</td>
<td>4.4.0-127</td>
<td>Nuevas imágenes de nodo trabajador con actualización del kernel para [CVE-2018-3639 ![Icono de enlace externo](../icons/launch-glyph.svg "Icono de enlace externo")](http://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2018-3639).</td>
</tr>
</tbody>
</table>



### Registro de cambios para el fix pack de nodo trabajador 1.10.1_1510, publicado el 18 de mayo de 2018
{: #1101_1510}

<table summary="Cambios realizados desde la versión 1.10.1_1509">
<caption>Cambios desde la versión 1.10.1_1509</caption>
<thead>
<tr>
<th>Componente</th>
<th>Anterior</th>
<th>Actual</th>
<th>Descripción</th>
</tr>
</thead>
<tbody>
<tr>
<td>Kubelet</td>
<td>N/D</td>
<td>N/D</td>
<td>Corregido un error que se producía al utilizar el plugin de almacenamiento en bloques.</td>
</tr>
</tbody>
</table>

### Registro de cambios para el fix pack de nodo trabajador 1.10.1_1509, publicado el 16 de mayo de 2018
{: #1101_1509}

<table summary="Cambios realizados desde la versión 1.10.1_1508">
<caption>Cambios desde la versión 1.10.1_1508</caption>
<thead>
<tr>
<th>Componente</th>
<th>Anterior</th>
<th>Actual</th>
<th>Descripción</th>
</tr>
</thead>
<tbody>
<tr>
<td>Kubelet</td>
<td>N/D</td>
<td>N/D</td>
<td>Los datos que se almacenan en el `kubelet` del directorio raíz se guardan ahora en el disco secundario más grande de la máquina del nodo trabajador.</td>
</tr>
</tbody>
</table>

### Registro de cambios para 1.10.1_1508, publicado el 01 de mayo de 2018
{: #1101_1508}

<table summary="Cambios realizados desde la versión 1.9.7_1510">
<caption>Cambios desde la versión 1.9.7_1510</caption>
<thead>
<tr>
<th>Componente</th>
<th>Anterior</th>
<th>Actual</th>
<th>Descripción</th>
</tr>
</thead>
<tbody>
<tr>
<td>Calico</td>
<td>v2.6.5</td>
<td>v3.1.1</td>
<td>Consulte las [notas del release de Calico ![Icono de enlace externo](../icons/launch-glyph.svg "Icono de enlace externo")](https://docs.projectcalico.org/v3.1/releases/#v311).</td>
</tr>
<tr>
<td>Kubernetes Heapster</td>
<td>v1.5.0</td>
<td>v1.5.2</td>
<td>Consulte las [notas del release de Kubernetes Heapster ![Icono de enlace externo](../icons/launch-glyph.svg "Icono de enlace externo")](https://github.com/kubernetes/heapster/releases/tag/v1.5.2).</td>
</tr>
<tr>
<td>Kubernetes</td>
<td>v1.9.7</td>
<td>v1.10.1</td>
<td>Consulte las [notas del release de Kubernetes ![Icono de enlace externo](../icons/launch-glyph.svg "Icono de enlace externo")](https://github.com/kubernetes/kubernetes/releases/tag/v1.10.1).</td>
</tr>
<tr>
<td>Configuración de Kubernetes</td>
<td>N/D</td>
<td>N/D</td>
<td>Añadido <code>StorageObjectInUseProtection</code> a la opción <code>--enable-admission-plugins</code> para el servidor de API de Kubernetes del clúster.</td>
</tr>
<tr>
<td>DNS de Kubernetes</td>
<td>1.14.8</td>
<td>1.14.10</td>
<td>Consulte las [notas del release de DNS de Kubernetes ![Icono de enlace externo](../icons/launch-glyph.svg "Icono de enlace externo")](https://github.com/kubernetes/dns/releases/tag/1.14.10).</td>
</tr>
<tr>
<td>Proveedor de {{site.data.keyword.Bluemix_notm}}</td>
<td>v1.9.7-102</td>
<td>v1.10.1-52</td>
<td>Actualizado para dar soporte al release 1.10 de Kubernetes.</td>
</tr>
<tr>
<td>Soporte de GPU</td>
<td>N/D</td>
<td>N/D</td>
<td>Ahora hay disponible soporte para [cargas de trabajo de contenedor con unidad de proceso de gráficos (GPU)](cs_app.html#gpu_app) para su planificación y ejecución. Para obtener una lista de los tipos de máquina con GPU que hay disponibles, consulte [Hardware para nodos de trabajador](cs_clusters_planning.html#shared_dedicated_node). Para obtener más información, consulte la documentación de Kubernetes de [planificación de GPU ![Icono de enlace externo](../icons/launch-glyph.svg "Icono de enlace externo")](https://kubernetes.io/docs/tasks/manage-gpus/scheduling-gpus/).</td>
</tr>
</tbody>
</table>

<br />


## Registro de cambios de la versión 1.9
{: #19_changelog}

Revise los siguientes cambios.

### Registro de cambios para fixpack de nodo maestro 1.9.10_1530, publicado el 15 de octubre de 2018
{: #1910_1530}

<table summary="Cambios realizados desde la versión 1.9.10_1527">
<caption>Cambios desde la versión 1.9.10_1527</caption>
<thead>
<tr>
<th>Componente</th>
<th>Anterior</th>
<th>Actual</th>
<th>Descripción</th>
</tr>
</thead>
<tbody>
<tr>
<td>Actualización de clúster</td>
<td>N/D</td>
<td>N/D</td>
<td>Se ha corregido el problema con la actualización de los complementos de clúster cuando el nodo maestro se actualiza desde una versión no soportada.</td>
</tr>
</tbody>
</table>

### Registro de cambios para el fix pack de nodo trabajador 1.9.10_1528, publicado el 10 de octubre de 2018
{: #1910_1528}

<table summary="Cambios realizados desde la versión 1.9.10_1527">
<caption>Cambios desde la versión 1.9.10_1527</caption>
<thead>
<tr>
<th>Componente</th>
<th>Anterior</th>
<th>Actual</th>
<th>Descripción</th>
</tr>
</thead>
<tbody>
<tr>
<td>Kernel</td>
<td>4.4.0-133</td>
<td>4.4.0-137</td>
<td>Se han actualizado las imágenes de nodo trabajador con la actualización de kernel para [CVE-2018-14633, CVE-2018-17182 ![Icono de enlace externo](../icons/launch-glyph.svg "Icono de enlace externo")](https://changelogs.ubuntu.com/changelogs/pool/main/l/linux/linux_4.4.0-137.163/changelog).</td>
</tr>
<tr>
<td>Tiempo de espera de sesión inactiva</td>
<td>N/D</td>
<td>N/D</td>
<td>Establezca el tiempo de espera de sesión inactiva en 5 minutos por razones de conformidad.</td>
</tr>
</tbody>
</table>


### Registro de cambios para 1.9.10_1527, publicado el 2 de octubre de 2018
{: #1910_1527}

<table summary="Cambios realizados desde la versión 1.9.10_1523">
<caption>Cambios desde la versión 1.9.10_1523</caption>
<thead>
<tr>
<th>Componente</th>
<th>Anterior</th>
<th>Actual</th>
<th>Descripción</th>
</tr>
</thead>
<tbody>
<tr>
<td>Proveedor de {{site.data.keyword.Bluemix_notm}}</td>
<td>v1.9.10-192</td>
<td>v1.9.10-219</td>
<td>Se ha actualizado el enlace de la documentación en los mensajes de error del equilibrador de carga.</td>
</tr>
<tr>
<td>Clases de almacenamiento de archivos de IBM</td>
<td>N/D</td>
<td>N/D</td>
<td>Se ha eliminado `mountOptions` en las clases de almacenamiento de archivos de IBM para utilizar el valor predeterminado que proporciona el nodo trabajador. Se ha eliminado el parámetro `reclaimPolicy` duplicado de las clases de almacenamiento de archivos de IBM.<br><br>
Además, ahora, cuando actualiza el nodo maestro del clúster, la clase de almacenamiento de archivos predeterminada de IBM no se modifica. Si desea cambiar la clase de almacenamiento predeterminada, ejecute el mandato `kubectl parche storageclass <storageclass> -p '{"metadata": {"annotations":{"storageclass.kubernetes.io/is-default-class":"true"}}}'` y sustituya `<storageclass>` por el nombre de la clase de almacenamiento.</td>
</tr>
</tbody>
</table>

### Registro de cambios para el fix pack de nodo trabajador 1.9.10_1524, publicado el 20 de septiembre de 2018
{: #1910_1524}

<table summary="Cambios realizados desde la versión 1.9.10_1523">
<caption>Cambios desde la versión 1.9.10_1523</caption>
<thead>
<tr>
<th>Componente</th>
<th>Anterior</th>
<th>Actual</th>
<th>Descripción</th>
</tr>
</thead>
<tbody>
<tr>
<td>Rotación de registros</td>
<td>N/D</td>
<td>N/D</td>
<td>Se ha modificado para utilizar temporizadores `systemd` en lugar de `cronjobs` para evitar que `logrotate` falle en los nodos trabajadores que no se han vuelto a cargar o no se han actualizado en 90 días. **Nota**: en
todas las versiones anteriores de este release menor, el disco primario se llenaba después de que fallar el trabajo cron porque los registros no se rotaban. El trabajo cron falla después de que el nodo trabajador esté activo durante 90 días sin que se haya actualizado o recargado. Si los registros llenan todo el disco primario, el nodo trabajador entra en un estado de error. El nodo trabajador se puede arreglar mediante el [mandato](cs_cli_reference.html#cs_worker_reload) `ibmcloud ks worker-reload` o el [mandato](cs_cli_reference.html#cs_worker_update) `ibmcloud ks worker-update`.</td>
</tr>
<tr>
<td>Componentes de tiempo de ejecución de nodo trabajador (`kubelet`, `kube-proxy`, `docker`)</td>
<td>N/D</td>
<td>N/D</td>
<td>Se han eliminado las dependencias de los componentes de tiempo de ejecución en el disco primario. Esta mejora impide que los nodos trabajadores fallen cuando se llena el disco primario.</td>
</tr>
<tr>
<td>Caducidad de la contraseña raíz</td>
<td>N/D</td>
<td>N/D</td>
<td>Las contraseñas raíz para los nodos trabajadores caducan después de 90 días por razones de conformidad. Si las herramientas de automatización tienen que iniciar la sesión en el nodo trabajador como usuario root o se basan en trabajos cron que se ejecutan como root, puede inhabilitar la caducidad de la contraseña iniciando una sesión en el nodo de trabajo y ejecutando `chage -M -1 root`. **Nota**: si tiene requisitos de conformidad de seguridad que impiden la ejecución como root o la eliminación de la caducidad de la contraseña, no inhabilite la caducidad. En lugar de ello, puede [actualizar](cs_cli_reference.html#cs_worker_update) o [volver a cargar](cs_cli_reference.html#cs_worker_reload) los nodos trabajadores al menos cada 90 días.</td>
</tr>
<tr>
<td>Systemd</td>
<td>N/D</td>
<td>N/D</td>
<td>Limpie de forma periódica las unidades de montaje transitorias para evitar que se desborden. Esta acción está relacionada con el [problema de Kubernetes 57345 ![Icono de enlace externo](../icons/launch-glyph.svg "Icono de enlace externo")](https://github.com/kubernetes/kubernetes/issues/57345).</td>
</tr>
<tr>
<td>Docker</td>
<td>N/D</td>
<td>N/D</td>
<td>Inhabilite el puente de Docker predeterminado para que se utilice el rango de IP `172.17.0.0/16` para las rutas privadas. Si crea los contenedores Docker en los nodos trabajadores ejecutando los mandatos `docker` en el host directamente o utilizando un pod que monta el socket de Docker, elija una de las opciones siguientes.<ul><li>Para garantizar la conectividad de red externa al crear el contenedor, ejecute `docker build . --network host`.</li>
<li>Para crear de forma explícita una red para utilizarla al crear el contenedor, ejecute `docker network create` y luego utilice esta red.</li></ul>
**Nota**: ¿Tiene dependencias en el socket Docker o Docker directamente? [Mire a `containerd` en lugar de a `docker` como entorno de ejecución del contenedor](cs_versions.html#containerd) para que los clústeres estén preparados para ejecutar Kubernetes versión 1.11 o posteriores.</td>
</tr>
</tbody>
</table>

### Registro de cambios para 1.9.10_1523, publicado el 4 de septiembre de 2018
{: #1910_1523}

<table summary="Cambios realizados desde la versión 1.9.9_1522">
<caption>Cambios desde la versión 1.9.9_1522</caption>
<thead>
<tr>
<th>Componente</th>
<th>Anterior</th>
<th>Actual</th>
<th>Descripción</th>
</tr>
</thead>
<tbody>
<tr>
<td>Proveedor de {{site.data.keyword.Bluemix_notm}}</td>
<td>v1.9.9-167</td>
<td>v1.9.10-192</td>
<td>Actualizado para dar soporte al release 1.9.10 de Kubernetes. Además, se ha cambiado la configuración del proveedor de nube para manejar mejor las actualizaciones para los servicios de equilibrador de carga con `externalTrafficPolicy` establecido en `local`.</td>
</tr>
<tr>
<td>Plugin de almacenamiento de archivos de IBM</td>
<td>334</td>
<td>338</td>
<td>Se ha actualizado la versión de incubator a 1.8. El almacenamiento de archivos se suministra a la zona específica que seleccione. No puede actualizar las etiquetas de una instancia de PV existente (estática) a menos que esté utilizando un clúster multizona y tenga que añadir las etiquetas de zona y de región.<br><br>Se ha eliminado la versión de NFS predeterminada de las opciones de montaje de las clases de almacenamiento de archivos proporcionadas por IBM. El sistema operativo del host ahora negocia la versión de NFS con el servidor NFS de la infraestructura de IBM Cloud (SoftLayer). Para establecer manualmente una versión de NFS específica, o para cambiar la versión de NFS de su PV que ha sido negociada por el sistema operativo del host, consulte [Cambio de la versión predeterminada de NFS](cs_storage_file.html#nfs_version_class).</td>
</tr>
<tr>
<td>Kubernetes</td>
<td>v1.9.9</td>
<td>v1.9.10</td>
<td>Consulte las [notas del release de Kubernetes ![Icono de enlace externo](../icons/launch-glyph.svg "Icono de enlace externo")](https://github.com/kubernetes/kubernetes/releases/tag/v1.9.10).</td>
</tr>
<tr>
<td>Configuración de Kubernetes Heapster</td>
<td>N/D</td>
<td>N/D</td>
<td>Se han aumentado los límites de recursos para el contenedor `heapster-nanny`.</td>
</tr>
</tbody>
</table>

### Registro de cambios para el fix pack de nodo trabajador 1.9.9_1522, publicado el 23 de agosto de 2018
{: #199_1522}

<table summary="Cambios realizados desde la versión 1.9.9_1521">
<caption>Cambios desde la versión 1.9.9_1521</caption>
<thead>
<tr>
<th>Componente</th>
<th>Anterior</th>
<th>Actual</th>
<th>Descripción</th>
</tr>
</thead>
<tbody>
<tr>
<td>`systemd`</td>
<td>229</td>
<td>230</td>
<td>Se ha actualizado `systemd` para arreglar la fuga de `cgroup`.</td>
</tr>
<tr>
<td>Kernel</td>
<td>4.4.0-127</td>
<td>4.4.0-133</td>
<td>Se han actualizado las imágenes de nodo trabajador con la actualización de kernel para [CVE-2018-3620, CVE-2018-3646 ![Icono de enlace externo](../icons/launch-glyph.svg "Icono de enlace externo")](https://usn.ubuntu.com/3741-1/).</td>
</tr>
</tbody>
</table>


### Registro de cambios para el fix pack de nodo trabajador 1.9.9_1521, publicado el 13 de agosto de 2018
{: #199_1521}

<table summary="Cambios realizados desde la versión 1.9.9_1520">
<caption>Cambios desde la versión 1.9.9_1520</caption>
<thead>
<tr>
<th>Componente</th>
<th>Anterior</th>
<th>Actual</th>
<th>Descripción</th>
</tr>
</thead>
<tbody>
<tr>
<td>Paquetes Ubuntu</td>
<td>N/D</td>
<td>N/D</td>
<td>Actualizaciones de los paquetes de Ubuntu instalados.</td>
</tr>
</tbody>
</table>

### Registro de cambios para 1.9.9_1520, publicado el 27 de julio de 2018
{: #199_1520}

<table summary="Cambios realizados desde la versión 1.9.8_1517">
<caption>Cambios desde la versión 1.9.8_1517</caption>
<thead>
<tr>
<th>Componente</th>
<th>Anterior</th>
<th>Actual</th>
<th>Descripción</th>
</tr>
</thead>
<tbody>
<tr>
<td>Proveedor de {{site.data.keyword.Bluemix_notm}}</td>
<td>v1.9.8-141</td>
<td>v1.9.9-167</td>
<td>Actualizado para dar soporte al release 1.9.9 de Kubernetes. Además, ahora los sucesos del servicio de LoadBalancer `create failure` incluyen cualquier error de subred portátil.</td>
</tr>
<tr>
<td>Plugin de almacenamiento de archivos de IBM</td>
<td>320</td>
<td>334</td>
<td>Se ha aumentado el tiempo de espera para la creación de un volumen persistente de 15 a 30 minutos. Se ha cambiado el tipo de facturación predeterminado a `por hora`. Se han añadido opciones de montaje a las clases de almacenamiento predefinidas. En la instancia de almacenamiento de archivos NFS de la cuenta de infraestructura de IBM Cloud (SoftLayer), se ha cambiado el campo **Notas** por el formato JSON y se ha añadido el espacio de nombres de Kubernetes en el que se ha desplegado el PV. Para dar soporte a clústeres multizona, se han añadido etiquetas de zona y región a los volúmenes persistentes.</td>
</tr>
<tr>
<td>Kubernetes</td>
<td>v1.9.8</td>
<td>v1.9.9</td>
<td>Consulte las [notas del release de Kubernetes ![Icono de enlace externo](../icons/launch-glyph.svg "Icono de enlace externo")](https://github.com/kubernetes/kubernetes/releases/tag/v1.9.9).</td>
</tr>
<tr>
<td>Kernel</td>
<td>N/D</td>
<td>N/D</td>
<td>Mejoras menores en los valores de red del nodo trabajador para las cargas de trabajo de red de alto rendimiento.</td>
</tr>
<tr>
<td>Cliente OpenVPN</td>
<td>N/D</td>
<td>N/D</td>
<td>El despliegue de cliente de OpenVPN `vpn` que se ejecuta en el espacio de nombres `kube-system` ahora se gestiona mediante `addon-manager` de Kubernetes.</td>
</tr>
</tbody>
</table>

### Registro de cambios para el fix pack de nodo trabajador 1.9.8_1517, publicado el 3 de julio de 2018
{: #198_1517}

<table summary="Cambios realizados desde la versión 1.9.8_1516">
<caption>Cambios desde la versión 1.9.8_1516</caption>
<thead>
<tr>
<th>Componente</th>
<th>Anterior</th>
<th>Actual</th>
<th>Descripción</th>
</tr>
</thead>
<tbody>
<tr>
<td>Kernel</td>
<td>N/D</td>
<td>N/D</td>
<td>Se ha optimizado `sysctl` para las cargas de trabajo de red de alto rendimiento.</td>
</tr>
</tbody>
</table>


### Registro de cambios para el fix pack de nodo trabajador 1.9.8_1516, publicado el 21 de junio de 2018
{: #198_1516}

<table summary="Cambios realizados desde la versión 1.9.8_1515">
<caption>Cambios desde la versión 1.9.8_1515</caption>
<thead>
<tr>
<th>Componente</th>
<th>Anterior</th>
<th>Actual</th>
<th>Descripción</th>
</tr>
</thead>
<tbody>
<tr>
<td>Docker</td>
<td>N/D</td>
<td>N/D</td>
<td>Para los tipos de máquina no cifrados, el disco secundario se limpia obteniendo un sistema de archivos nuevo cuando se vuelve a cargar o se actualiza el nodo trabajador.</td>
</tr>
</tbody>
</table>

### Registro de cambios para 1.9.8_1515, publicado el 19 de junio de 2018
{: #198_1515}

<table summary="Cambios realizados desde la versión 1.9.7_1513">
<caption>Cambios desde la versión 1.9.7_1513</caption>
<thead>
<tr>
<th>Componente</th>
<th>Anterior</th>
<th>Actual</th>
<th>Descripción</th>
</tr>
</thead>
<tbody>
<tr>
<td>Kubernetes</td>
<td>v1.9.7</td>
<td>v1.9.8</td>
<td>Consulte las [notas del release de Kubernetes ![Icono de enlace externo](../icons/launch-glyph.svg "Icono de enlace externo")](https://github.com/kubernetes/kubernetes/releases/tag/v1.9.8).</td>
</tr>
<tr>
<td>Configuración de Kubernetes</td>
<td>N/D</td>
<td>N/D</td>
<td>Se ha añadido PodSecurityPolicy a la opción --admiten-control para el servidor de API Kubernetes del clúster y ha configurado el clúster para dar soporte a políticas de seguridad de pod. Para obtener más información, consulte [Configuración de políticas de seguridad de pod](cs_psp.html).</td>
</tr>
<tr>
<td>Proveedor de IBM Cloud</td>
<td>v1.9.7-102</td>
<td>v1.9.8-141</td>
<td>Actualizado para dar soporte al release 1.9.8 de Kubernetes.</td>
</tr>
<tr>
<td>Cliente OpenVPN</td>
<td>N/D</td>
<td>N/D</td>
<td>Se ha añadido <code>livenessProbe</code> al despliegue de cliente de OpenVPN <code>vpn</code> que se ejecuta en el espacio de nombres <code>kube-system</code>.</td>
</tr>
</tbody>
</table>


### Registro de cambios para el fix pack de nodo trabajador 1.9.7_1513, publicado el 11 de junio de 2018
{: #197_1513}

<table summary="Cambios realizados desde la versión 1.9.7_1512">
<caption>Cambios desde la versión 1.9.7_1512</caption>
<thead>
<tr>
<th>Componente</th>
<th>Anterior</th>
<th>Actual</th>
<th>Descripción</th>
</tr>
</thead>
<tbody>
<tr>
<td>Actualización del kernel</td>
<td>4.4.0-116</td>
<td>4.4.0-127</td>
<td>Nuevas imágenes de nodo trabajador con actualización del kernel para [CVE-2018-3639 ![Icono de enlace externo](../icons/launch-glyph.svg "Icono de enlace externo")](http://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2018-3639).</td>
</tr>
</tbody>
</table>

### Registro de cambios para el fix pack de nodo trabajador 1.9.7_1512, publicado el 18 de mayo de 2018
{: #197_1512}

<table summary="Cambios realizados desde la versión 1.9.7_1511">
<caption>Cambios desde la versión 1.9.7_1511</caption>
<thead>
<tr>
<th>Componente</th>
<th>Anterior</th>
<th>Actual</th>
<th>Descripción</th>
</tr>
</thead>
<tbody>
<tr>
<td>Kubelet</td>
<td>N/D</td>
<td>N/D</td>
<td>Corregido un error que se producía al utilizar el plugin de almacenamiento en bloques.</td>
</tr>
</tbody>
</table>

### Registro de cambios para el fix pack de nodo trabajador 1.9.7_1511, publicado el 16 de mayo de 2018
{: #197_1511}

<table summary="Cambios realizados desde la versión 1.9.7_1510">
<caption>Cambios desde la versión 1.9.7_1510</caption>
<thead>
<tr>
<th>Componente</th>
<th>Anterior</th>
<th>Actual</th>
<th>Descripción</th>
</tr>
</thead>
<tbody>
<tr>
<td>Kubelet</td>
<td>N/D</td>
<td>N/D</td>
<td>Los datos que se almacenan en el `kubelet` del directorio raíz se guardan ahora en el disco secundario más grande de la máquina del nodo trabajador.</td>
</tr>
</tbody>
</table>

### Registro de cambios para 1.9.7_1510, publicado el 30 de abril de 2018
{: #197_1510}

<table summary="Cambios realizados desde la versión 1.9.3_1506">
<caption>Cambios desde la versión 1.9.3_1506</caption>
<thead>
<tr>
<th>Componente</th>
<th>Anterior</th>
<th>Actual</th>
<th>Descripción</th>
</tr>
</thead>
<tbody>
<tr>
<td>Kubernetes</td>
<td>v1.9.3</td>
<td>v1.9.7	</td>
<td><p>Consulte las [notas del release de Kubernetes ![Icono de enlace externo](../icons/launch-glyph.svg "Icono de enlace externo")](https://github.com/kubernetes/kubernetes/releases/tag/v1.9.7). Este release corrige las vulnerabilidades [CVE-2017-1002101 ![Icono de enlace externo](../icons/launch-glyph.svg "Icono de enlace externo")](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2017-1002101) y [CVE-2017-1002102 ![Icono de enlace externo](../icons/launch-glyph.svg "Icono de enlace externo")](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2017-1002102).</p><p><strong>Nota</strong>: ahora se montan como de solo lectura los volúmenes proyectados, `secret`, `configMap` y `downwardAPI`. Anteriormente, las apps podían escribir datos en estos volúmenes, pero el sistema podía revertir automáticamente los datos. Si sus apps se basaban en este comportamiento inseguro anterior, modifíquelas en consecuencia.</p></td>
</tr>
<tr>
<td>Configuración de Kubernetes</td>
<td>N/D</td>
<td>N/D</td>
<td>Añadido `admissionregistration.k8s.io/v1alpha1=true` a la opción `--runtime-config` para el servidor de API de Kubernetes del clúster.</td>
</tr>
<tr>
<td>Proveedor de {{site.data.keyword.Bluemix_notm}}</td>
<td>v1.9.3-71</td>
<td>v1.9.7-102</td>
<td>Ahora los servicios `NodePort` y `LoadBalancer` dan soporte a la [conservación de la dirección IP de origen del cliente](cs_loadbalancer.html#node_affinity_tolerations) estableciendo `service.spec.externalTrafficPolicy` en `Local`.</td>
</tr>
<tr>
<td></td>
<td></td>
<td></td>
<td>Corregida la configuración de tolerancia del [nodo extremo](cs_edge.html#edge) en clústeres antiguos.</td>
</tr>
</tbody>
</table>

<br />


## Archivo
{: #changelog_archive}

Versiones no soportadas de Kubernetes:
*  [Versión 1.8](#18_changelog)
*  [Versión 1.7](#17_changelog)

### Registro de cambios de la versión 1.8 (no soportada)
{: #18_changelog}

Revise los siguientes cambios.

### Registro de cambios para el fix pack de nodo trabajador 1.8.15_1521, publicado el 20 de septiembre de 2018
{: #1815_1521}

<table summary="Cambios realizados desde la versión 1.8.15_1520">
<caption>Cambios desde la versión 1.8.15_1520</caption>
<thead>
<tr>
<th>Componente</th>
<th>Anterior</th>
<th>Actual</th>
<th>Descripción</th>
</tr>
</thead>
<tbody>
<tr>
<td>Rotación de registros</td>
<td>N/D</td>
<td>N/D</td>
<td>Se ha modificado para utilizar temporizadores `systemd` en lugar de `cronjobs` para evitar que `logrotate` falle en los nodos trabajadores que no se han vuelto a cargar o no se han actualizado en 90 días. **Nota**: en
todas las versiones anteriores de este release menor, el disco primario se llenaba después de que fallar el trabajo cron porque los registros no se rotaban. El trabajo cron falla después de que el nodo trabajador esté activo durante 90 días sin que se haya actualizado o recargado. Si los registros llenan todo el disco primario, el nodo trabajador entra en un estado de error. El nodo trabajador se puede arreglar mediante el [mandato](cs_cli_reference.html#cs_worker_reload) `ibmcloud ks worker-reload` o el [mandato](cs_cli_reference.html#cs_worker_update) `ibmcloud ks worker-update`.</td>
</tr>
<tr>
<td>Componentes de tiempo de ejecución de nodo trabajador (`kubelet`, `kube-proxy`, `docker`)</td>
<td>N/D</td>
<td>N/D</td>
<td>Se han eliminado las dependencias de los componentes de tiempo de ejecución en el disco primario. Esta mejora impide que los nodos trabajadores fallen cuando se llena el disco primario.</td>
</tr>
<tr>
<td>Caducidad de la contraseña raíz</td>
<td>N/D</td>
<td>N/D</td>
<td>Las contraseñas raíz para los nodos trabajadores caducan después de 90 días por razones de conformidad. Si las herramientas de automatización tienen que iniciar la sesión en el nodo trabajador como usuario root o se basan en trabajos cron que se ejecutan como root, puede inhabilitar la caducidad de la contraseña iniciando una sesión en el nodo de trabajo y ejecutando `chage -M -1 root`. **Nota**: si tiene requisitos de conformidad de seguridad que impiden la ejecución como root o la eliminación de la caducidad de la contraseña, no inhabilite la caducidad. En lugar de ello, puede [actualizar](cs_cli_reference.html#cs_worker_update) o [volver a cargar](cs_cli_reference.html#cs_worker_reload) los nodos trabajadores al menos cada 90 días.</td>
</tr>
<tr>
<td>Systemd</td>
<td>N/D</td>
<td>N/D</td>
<td>Limpie de forma periódica las unidades de montaje transitorias para evitar que se desborden. Esta acción está relacionada con el [problema de Kubernetes 57345 ![Icono de enlace externo](../icons/launch-glyph.svg "Icono de enlace externo")](https://github.com/kubernetes/kubernetes/issues/57345).</td>
</tr>
</tbody>
</table>

### Registro de cambios para el fix pack de nodo trabajador 1.8.15_1520, publicado el 23 de agosto de 2018
{: #1815_1520}

<table summary="Cambios realizados desde la versión 1.8.15_1519">
<caption>Cambios desde la versión 1.8.15_1519</caption>
<thead>
<tr>
<th>Componente</th>
<th>Anterior</th>
<th>Actual</th>
<th>Descripción</th>
</tr>
</thead>
<tbody>
<tr>
<td>`systemd`</td>
<td>229</td>
<td>230</td>
<td>Se ha actualizado `systemd` para arreglar la fuga de `cgroup`.</td>
</tr>
<tr>
<td>Kernel</td>
<td>4.4.0-127</td>
<td>4.4.0-133</td>
<td>Se han actualizado las imágenes de nodo trabajador con la actualización de kernel para [CVE-2018-3620, CVE-2018-3646 ![Icono de enlace externo](../icons/launch-glyph.svg "Icono de enlace externo")](https://usn.ubuntu.com/3741-1/).</td>
</tr>
</tbody>
</table>

### Registro de cambios para el fix pack de nodo trabajador 1.8.15_1519, publicado el 13 de agosto de 2018
{: #1815_1519}

<table summary="Cambios realizados desde la versión 1.8.15_1518">
<caption>Cambios desde la versión 1.8.15_1518</caption>
<thead>
<tr>
<th>Componente</th>
<th>Anterior</th>
<th>Actual</th>
<th>Descripción</th>
</tr>
</thead>
<tbody>
<tr>
<td>Paquetes Ubuntu</td>
<td>N/D</td>
<td>N/D</td>
<td>Actualizaciones de los paquetes de Ubuntu instalados.</td>
</tr>
</tbody>
</table>

### Registro de cambios para 1.8.15_1518, publicado el 27 de julio de 2018
{: #1815_1518}

<table summary="Cambios realizados desde la versión 1.8.13_1516">
<caption>Cambios desde la versión 1.8.13_1516</caption>
<thead>
<tr>
<th>Componente</th>
<th>Anterior</th>
<th>Actual</th>
<th>Descripción</th>
</tr>
</thead>
<tbody>
<tr>
<td>Proveedor de {{site.data.keyword.Bluemix_notm}}</td>
<td>v1.8.13-176</td>
<td>v1.8.15-204</td>
<td>Actualizado para dar soporte al release 1.8.15 de Kubernetes. Además, ahora los sucesos del servicio de LoadBalancer `create failure` incluyen cualquier error de subred portátil.</td>
</tr>
<tr>
<td>Plugin de almacenamiento de archivos de IBM</td>
<td>320</td>
<td>334</td>
<td>Se ha aumentado el tiempo de espera para la creación de un volumen persistente de 15 a 30 minutos. Se ha cambiado el tipo de facturación predeterminado a `por hora`. Se han añadido opciones de montaje a las clases de almacenamiento predefinidas. En la instancia de almacenamiento de archivos NFS de la cuenta de infraestructura de IBM Cloud (SoftLayer), se ha cambiado el campo **Notas** por el formato JSON y se ha añadido el espacio de nombres de Kubernetes en el que se ha desplegado el PV. Para dar soporte a clústeres multizona, se han añadido etiquetas de zona y región a los volúmenes persistentes.</td>
</tr>
<tr>
<td>Kubernetes</td>
<td>v1.8.13</td>
<td>v1.8.15</td>
<td>Consulte las [notas del release de Kubernetes ![Icono de enlace externo](../icons/launch-glyph.svg "Icono de enlace externo")](https://github.com/kubernetes/kubernetes/releases/tag/v1.8.15).</td>
</tr>
<tr>
<td>Kernel</td>
<td>N/D</td>
<td>N/D</td>
<td>Mejoras menores en los valores de red del nodo trabajador para las cargas de trabajo de red de alto rendimiento.</td>
</tr>
<tr>
<td>Cliente OpenVPN</td>
<td>N/D</td>
<td>N/D</td>
<td>El despliegue de cliente de OpenVPN `vpn` que se ejecuta en el espacio de nombres `kube-system` ahora se gestiona mediante `addon-manager` de Kubernetes.</td>
</tr>
</tbody>
</table>

### Registro de cambios para el fix pack de nodo trabajador 1.8.13_1516, publicado el 3 de julio de 2018
{: #1813_1516}

<table summary="Cambios realizados desde la versión 1.8.13_1515">
<caption>Cambios desde la versión 1.8.13_1515</caption>
<thead>
<tr>
<th>Componente</th>
<th>Anterior</th>
<th>Actual</th>
<th>Descripción</th>
</tr>
</thead>
<tbody>
<tr>
<td>Kernel</td>
<td>N/D</td>
<td>N/D</td>
<td>Se ha optimizado `sysctl` para las cargas de trabajo de red de alto rendimiento.</td>
</tr>
</tbody>
</table>


### Registro de cambios para el fix pack de nodo trabajador 1.8.13_1515, publicado el 21 de junio de 2018
{: #1813_1515}

<table summary="Cambios realizados desde la versión 1.8.13_1514">
<caption>Cambios desde la versión 1.8.13_1514</caption>
<thead>
<tr>
<th>Componente</th>
<th>Anterior</th>
<th>Actual</th>
<th>Descripción</th>
</tr>
</thead>
<tbody>
<tr>
<td>Docker</td>
<td>N/D</td>
<td>N/D</td>
<td>Para los tipos de máquina no cifrados, el disco secundario se limpia obteniendo un sistema de archivos nuevo cuando se vuelve a cargar o se actualiza el nodo trabajador.</td>
</tr>
</tbody>
</table>

### Registro de cambios para 1.8.13_1514, publicado el 19 de junio de 2018
{: #1813_1514}

<table summary="Cambios realizados desde la versión 1.8.11_1512">
<caption>Cambios desde la versión 1.8.11_1512</caption>
<thead>
<tr>
<th>Componente</th>
<th>Anterior</th>
<th>Actual</th>
<th>Descripción</th>
</tr>
</thead>
<tbody>
<tr>
<td>Kubernetes</td>
<td>v1.8.11</td>
<td>v1.8.13</td>
<td>Consulte las [notas del release de Kubernetes ![Icono de enlace externo](../icons/launch-glyph.svg "Icono de enlace externo")](https://github.com/kubernetes/kubernetes/releases/tag/v1.8.13).</td>
</tr>
<tr>
<td>Configuración de Kubernetes</td>
<td>N/D</td>
<td>N/D</td>
<td>Se ha añadido PodSecurityPolicy a la opción --admiten-control para el servidor de API Kubernetes del clúster y ha configurado el clúster para dar soporte a políticas de seguridad de pod. Para obtener más información, consulte [Configuración de políticas de seguridad de pod](cs_psp.html).</td>
</tr>
<tr>
<td>Proveedor de IBM Cloud</td>
<td>v1.8.11-126</td>
<td>v1.8.13-176</td>
<td>Actualizado para dar soporte al release 1.8.13 de Kubernetes.</td>
</tr>
<tr>
<td>Cliente OpenVPN</td>
<td>N/D</td>
<td>N/D</td>
<td>Se ha añadido <code>livenessProbe</code> al despliegue de cliente de OpenVPN <code>vpn</code> que se ejecuta en el espacio de nombres <code>kube-system</code>.</td>
</tr>
</tbody>
</table>


### Registro de cambios para el fix pack de nodo trabajador 1.8.11_1512, publicado el 11 de junio de 2018
{: #1811_1512}

<table summary="Cambios realizados desde la versión 1.8.11_1511">
<caption>Cambios desde la versión 1.8.11_1511</caption>
<thead>
<tr>
<th>Componente</th>
<th>Anterior</th>
<th>Actual</th>
<th>Descripción</th>
</tr>
</thead>
<tbody>
<tr>
<td>Actualización del kernel</td>
<td>4.4.0-116</td>
<td>4.4.0-127</td>
<td>Nuevas imágenes de nodo trabajador con actualización del kernel para [CVE-2018-3639 ![Icono de enlace externo](../icons/launch-glyph.svg "Icono de enlace externo")](http://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2018-3639).</td>
</tr>
</tbody>
</table>


### Registro de cambios para el fix pack de nodo trabajador 1.8.11_1511, publicado el 18 de mayo de 2018
{: #1811_1511}

<table summary="Cambios realizados desde la versión 1.8.11_1510">
<caption>Cambios desde la versión 1.8.11_1510</caption>
<thead>
<tr>
<th>Componente</th>
<th>Anterior</th>
<th>Actual</th>
<th>Descripción</th>
</tr>
</thead>
<tbody>
<tr>
<td>Kubelet</td>
<td>N/D</td>
<td>N/D</td>
<td>Corregido un error que se producía al utilizar el plugin de almacenamiento en bloques.</td>
</tr>
</tbody>
</table>

### Registro de cambios para el fix pack de nodo trabajador 1.8.11_1510, publicado el 16 de mayo de 2018
{: #1811_1510}

<table summary="Cambios realizados desde la versión 1.8.11_1509">
<caption>Cambios desde la versión 1.8.11_1509</caption>
<thead>
<tr>
<th>Componente</th>
<th>Anterior</th>
<th>Actual</th>
<th>Descripción</th>
</tr>
</thead>
<tbody>
<tr>
<td>Kubelet</td>
<td>N/D</td>
<td>N/D</td>
<td>Los datos que se almacenan en el `kubelet` del directorio raíz se guardan ahora en el disco secundario más grande de la máquina del nodo trabajador.</td>
</tr>
</tbody>
</table>


### Registro de cambios para 1.8.11_1509, publicado el 19 de abril de 2018
{: #1811_1509}

<table summary="Cambios realizados desde la versión 1.8.8_1507">
<caption>Cambios desde la versión 1.8.8_1507</caption>
<thead>
<tr>
<th>Componente</th>
<th>Anterior</th>
<th>Actual</th>
<th>Descripción</th>
</tr>
</thead>
<tbody>
<tr>
<td>Kubernetes</td>
<td>v1.8.8</td>
<td>v1.8.11	</td>
<td><p>Consulte las [notas del release de Kubernetes ![Icono de enlace externo](../icons/launch-glyph.svg "Icono de enlace externo")](https://github.com/kubernetes/kubernetes/releases/tag/v1.8.11). Este release corrige las vulnerabilidades [CVE-2017-1002101 ![Icono de enlace externo](../icons/launch-glyph.svg "Icono de enlace externo")](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2017-1002101) y [CVE-2017-1002102 ![Icono de enlace externo](../icons/launch-glyph.svg "Icono de enlace externo")](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2017-1002102).</p><p><strong>Nota</strong>: ahora se montan como de solo lectura los volúmenes proyectados, `secret`, `configMap` y `downwardAPI`. Anteriormente, las apps podían escribir datos en estos volúmenes, pero el sistema podía revertir automáticamente los datos. Si sus apps se basaban en este comportamiento inseguro anterior, modifíquelas en consecuencia.</p></td>
</tr>
<tr>
<td>Imagen de contenedor en pausa</td>
<td>3.0</td>
<td>3.1</td>
<td>Elimina procesos zombie huérfanos heredados.</td>
</tr>
<tr>
<td>Proveedor de {{site.data.keyword.Bluemix_notm}}</td>
<td>v1.8.8-86</td>
<td>v1.8.11-126</td>
<td>Ahora los servicios `NodePort` y `LoadBalancer` dan soporte a la [conservación de la dirección IP de origen del cliente](cs_loadbalancer.html#node_affinity_tolerations) estableciendo `service.spec.externalTrafficPolicy` en `Local`.</td>
</tr>
<tr>
<td></td>
<td></td>
<td></td>
<td>Corregida la configuración de tolerancia del [nodo extremo](cs_edge.html#edge) en clústeres antiguos.</td>
</tr>
</tbody>
</table>

<br />


### Registro de cambios de la versión 1.7 (no soportada)
{: #17_changelog}

Revise los siguientes cambios.

#### Registro de cambios para el fix pack de nodo trabajador 1.7.16_1514, publicado el 11 de junio de 2018
{: #1716_1514}

<table summary="Cambios realizados desde la versión 1.7.16_1513">
<caption>Cambios desde la versión 1.7.16_1513</caption>
<thead>
<tr>
<th>Componente</th>
<th>Anterior</th>
<th>Actual</th>
<th>Descripción</th>
</tr>
</thead>
<tbody>
<tr>
<td>Actualización del kernel</td>
<td>4.4.0-116</td>
<td>4.4.0-127</td>
<td>Nuevas imágenes de nodo trabajador con actualización del kernel para [CVE-2018-3639 ![Icono de enlace externo](../icons/launch-glyph.svg "Icono de enlace externo")](http://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2018-3639).</td>
</tr>
</tbody>
</table>

#### Registro de cambios para el fix pack de nodo trabajador 1.7.16_1513, publicado el 18 de mayo de 2018
{: #1716_1513}

<table summary="Cambios realizados desde la versión 1.7.16_1512">
<caption>Cambios desde la versión 1.7.16_1512</caption>
<thead>
<tr>
<th>Componente</th>
<th>Anterior</th>
<th>Actual</th>
<th>Descripción</th>
</tr>
</thead>
<tbody>
<tr>
<td>Kubelet</td>
<td>N/D</td>
<td>N/D</td>
<td>Corregido un error que se producía al utilizar el plugin de almacenamiento en bloques.</td>
</tr>
</tbody>
</table>

#### Registro de cambios para el fix pack de nodo trabajador 1.7.16_1512, publicado el 16 de mayo de 2018
{: #1716_1512}

<table summary="Cambios realizados desde la versión 1.7.16_1511">
<caption>Cambios desde la versión 1.7.16_1511</caption>
<thead>
<tr>
<th>Componente</th>
<th>Anterior</th>
<th>Actual</th>
<th>Descripción</th>
</tr>
</thead>
<tbody>
<tr>
<td>Kubelet</td>
<td>N/D</td>
<td>N/D</td>
<td>Los datos que se almacenan en el `kubelet` del directorio raíz se guardan ahora en el disco secundario más grande de la máquina del nodo trabajador.</td>
</tr>
</tbody>
</table>

#### Registro de cambios para 1.7.16_1511, publicado el 19 de abril de 2018
{: #1716_1511}

<table summary="Cambios realizados desde la versión 1.7.4_1509">
<caption>Cambios desde la versión 1.7.4_1509</caption>
<thead>
<tr>
<th>Componente</th>
<th>Anterior</th>
<th>Actual</th>
<th>Descripción</th>
</tr>
</thead>
<tbody>
<tr>
<td>Kubernetes</td>
<td>v1.7.4</td>
<td>v1.7.16	</td>
<td><p>Consulte las [notas del release de Kubernetes ![Icono de enlace externo](../icons/launch-glyph.svg "Icono de enlace externo")](https://github.com/kubernetes/kubernetes/releases/tag/v1.7.16). Este release corrige las vulnerabilidades [CVE-2017-1002101 ![Icono de enlace externo](../icons/launch-glyph.svg "Icono de enlace externo")](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2017-1002101) y [CVE-2017-1002102 ![Icono de enlace externo](../icons/launch-glyph.svg "Icono de enlace externo")](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2017-1002102).</p><p><strong>Nota</strong>: ahora se montan como de solo lectura los volúmenes proyectados, `secret`, `configMap` y `downwardAPI`. Anteriormente, las apps podían escribir datos en estos volúmenes, pero el sistema podía revertir automáticamente los datos. Si sus apps se basaban en este comportamiento inseguro anterior, modifíquelas en consecuencia.</p></td>
</tr>
<td>Proveedor de {{site.data.keyword.Bluemix_notm}}</td>
<td>v1.7.4-133</td>
<td>v1.7.16-17</td>
<td>Ahora los servicios `NodePort` y `LoadBalancer` dan soporte a la [conservación de la dirección IP de origen del cliente](cs_loadbalancer.html#node_affinity_tolerations) estableciendo `service.spec.externalTrafficPolicy` en `Local`.</td>
</tr>
<tr>
<td></td>
<td></td>
<td></td>
<td>Corregida la configuración de tolerancia del [nodo extremo](cs_edge.html#edge) en clústeres antiguos.</td>
</tr>
</tbody>
</table>
