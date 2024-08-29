# Switch setup

### Create VLANS

```javascript
Switch>enable
Switch#configure terminal
Switch(config)#vlan 10,20,30,40,50,60,70
Switch(config-vlan)#exit
Switch(config)#do show vlan
```



### Setting up access and trunk ports.

**Для примера**&#x20;

Порты от e0/0 до e1/1 должны быть переведены в режим access.

Порты от e0/0 до e0/2 отвечают за VLAN 10.&#x20;

Порты от e1/0 до e1/1 отвечают за VLAN 20.

Порт e0/3 отвечает за VLAN 30.

порт e1/2 в режим trunk.

```javascript
Switch>en
Switch#conf t
Switch(config)#interface range e0/0-2
Switch(config-if-range)#switchport mode access
Switch(config-if-range)#switchport access vlan 10

Switch(config-if-range)#interface range e1/0-1
Switch(config-if-range)#switchport mode access
Switch(config-if-range)#switchport access vlan 20

Switch(config)#interface e0/3
Switch(config-if)#switchport mode access
Switch(config-if)#switchport access vlan 30

Switch(config-if-range)#interface e1/2
Switch(config-if)#switchport trunk encapsulation dot1q
Switch(config-if)#switchport mode trunk
Switch(config-if)#do write
```

Для проверки правильности настройки введем следующую команду: Switch`#show int switchport`

* **show interface** _{eX/X}_ **switchport** - cтатус интерфейсов, включая VLAN которым они принадлежат. Будет выведена информация об отдельном интерфейсе, если он указан, или о всех сразу.

Убедимся, что поля `Administrative Mode` и `Operational Mode` находятся в режиме `static access` или `trunk` в зависимости от интерфейса, а так же на access портах настроен правильно VLAN (поле `Access Mode VLAN`)



### Настройка VTP

```javascript
Switch(config)#vtp domain SERVER
Switch(config)#vtp version 3
Switch(config)#exit
Switch#vtp primary vlan
```

* **vtp domain** _name_ - установка имени VTP-домена.
* **vtp version 3** - включения vtp версии 3.
* **vtp primary vlan** - сделать сервер primary.

Для всех остальных коммутаторов указываем **vtp mode client**.
