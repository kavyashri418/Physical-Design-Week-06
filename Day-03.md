## Design Library Cell using Magic Layout and ngspice Characterization

## 1 Inception of Layout - CMOS Fabrication Process

16-Mask CMOS Process
A 16-mask CMOS process refers to a fabrication flow that uses 16 photolithography masks to define wells, gates, implants, contacts, interconnects, and passivation. Each mask corresponds to a specific patterning step that shapes the electrical and structural features of the device. The process begins with well formation, followed by active area definition, gate oxide growth, and polysilicon gate patterning. Subsequent masks enable lightly doped drain (LDD) formation, source/drain implantation, and contact opening. The remaining masks are used for metal interconnect layers, vias between metals, final passivation, and pad opening. By the end of the 16-mask sequence, both NMOS and PMOS transistors are fully formed and interconnected, resulting in a complete CMOS integrated circuit ready for packaging.

Steps:
 - Selecting a substrate with suitable properties
 - Creating Active Region for the transistors
 - N-Well and P-Well Formation
 - Formation of Gate
 - Lightly-Doped Drain (LDD) Formation
 - Source and Drain Formation
 - Formation of Contacts and Local Interconnects
 - Formation of Higher Level Metal Layers 

## 1.1 Selecting a substrate with suitable properties
- P-type substrate with high resistivity (5~50ohms)
- Orientation (100)
- Substrate doping should be less than the well doping

<img width="1551" height="488" alt="Screenshot 2025-10-31 001318" src="https://github.com/user-attachments/assets/4f3c520d-c408-4460-8cf8-4fe50618832b" />

## 1.2 Creating Active Region for the transistors
- ~ 1um photoresist
- ~ 80nm of Si₃N₄
- ~ 40nm of SiO₂
- Washed out in developing solution Si₃N₄ etched.
- Resist chemically removed
- Placed in oxidation furnance
- Field oxide is grown this process is called "Locos" (Local Oxidation of Silicon)
- Si₃N₄ stripped using hot phosphoric acid

![Web_Photo_Editor (3)](https://github.com/user-attachments/assets/22e99851-fef8-4628-8586-533f28d502a7)

## 1.3 N-well and P-well Formation
- Ion-implantation is used to further change the channel doping to adjust the threshold voltage, as required.

![Web_Photo_Editor (4)](https://github.com/user-attachments/assets/46cf7e73-909d-415a-b7f6-9ec900748b1f)

## 1.4 Formation of Gate

![Web_Photo_Editor (5)](https://github.com/user-attachments/assets/858b2c00-0a40-45bd-8f51-15c36a32fcb5)
![Web_Photo_Editor (5)](https://github.com/user-attachments/assets/3f9b573e-8ace-4f50-87c7-a91f7a19108f)

## 1.5 Lightly-Doped Drain (LDD) Formation
- LDD is formed to prevent hot electron effect and short channel effects.
  PMOS Doping profile: P+, P-, N
  NMOS doping profile: N+, N-, P
Two reasons for this
- Hot electron effect - Electric Field E = v/d High energy carriers break Si-Si bonds 3.2ev barrier between Si conduction band.
- Short channel effect - for short channel drain field penerates channel.

![Web_Photo_Editor (6)](https://github.com/user-attachments/assets/e0ec1985-a85c-4f23-a3f5-87ae004400d8)

## 1.6 Source and Drain Formation

![Web_Photo_Editor (7)](https://github.com/user-attachments/assets/04b1454e-2034-4e6d-af10-5edaf96f3801)

## 1.7 Formation of Contacts and Local Interconnects

![Web_Photo_Editor (8)](https://github.com/user-attachments/assets/c8a1a26d-1da0-41ae-a47f-b2b87fb56774)
![Web_Photo_Editor (9)](https://github.com/user-attachments/assets/ca678fc8-37ce-4d12-b16f-15e88b760f7b)

## 1.8 Formation of Higher Level Metal Layers

![Web_Photo_Editor (11)](https://github.com/user-attachments/assets/362cce10-a8be-4272-8360-be68aea609e7)
![Web_Photo_Editor (12)](https://github.com/user-attachments/assets/b4d3dbe9-7fe7-4384-9b1a-b977d2e73c6a)

## 1.9 Final Wafer after Fabrication

<img width="1251" height="1016" alt="Screenshot 2025-11-16 210609" src="https://github.com/user-attachments/assets/ac2afeef-0c0f-4549-8a1e-029b0347ad32" />

<img width="1041" height="705" alt="image" src="https://github.com/user-attachments/assets/3c1d84e7-e2db-4d18-9a0e-3e3bc8824f44" />

## LAB-03 Create a SPICE deck to run a inverter transient simulation using ngspice

Edited spice file for ngspice simulation

<img width="1280" height="768" alt="image" src="https://github.com/user-attachments/assets/36bb1af4-e02f-4eba-8e3e-4178a69c8389" />

Commands for ngspice simulation
```
# Command to directly load spice file for simulation to ngspice
ngspice sky130_inv.spice

# Now that we have entered ngspice with the simulation spice file loaded we just have to load the plot
plot y vs time a
```

<img width="1280" height="768" alt="image" src="https://github.com/user-attachments/assets/53c92c28-4216-4a31-b185-476c0f7b494f" />

### Trans simulation results with Waveform

<img width="1280" height="768" alt="image" src="https://github.com/user-attachments/assets/4407e5fa-c4c3-40d8-a1cc-75156cd34843" />

## LAB-3.1 Introduction to DRC using Magic tool

- The Design Rules for Skywater 130nm technology can be found here:https://skywater-pdk.readthedocs.io/en/main/rules.html

<img width="1809" height="949" alt="Screenshot 2025-11-18 185111" src="https://github.com/user-attachments/assets/7f84904e-9bbb-450c-ace3-a42e9f080690" />


- Obtain the tutorial files for DRC labs from the following link:
  
```
wget http://opencircuitdesign.com/open_pdks/archive/drc_tests.tgz
tar xfz drc_tests.tgz
cd drc_tests
ls -al
vi .magicrc
magic -d XR &
```

<img width="1280" height="768" alt="image" src="https://github.com/user-attachments/assets/61d5470a-73b4-4d38-96f2-fbcb201b8302" />
<img width="1280" height="768" alt="image" src="https://github.com/user-attachments/assets/ad93c528-0fda-40c1-9570-91dead26f62e" />
<img width="1280" height="768" alt="image" src="https://github.com/user-attachments/assets/637d542d-da55-4a94-ba8e-de003d324ea4" />

## LAB-1 DRC: met3.mag
- To open Magic using OpenGL or Cairo graphical interfaces, invoke magic using the -d option:
```
For OpenGL: magic -d XR &
For Cairo: magic -d OGL &
```
- Open the met3.mag tutorial file in Magic either via the command line or from the GUI via File -> Open
- Now check the DRC errors in a specific area

Commands to check DRC
```
# To select the area
select area

# Must re-run drc check to see updated drc errors
drc check

# Selecting region displaying the new errors and getting the error messages 
drc why

# Metal of which we have select the area
goto m3.1
```

<img width="1280" height="768" alt="image" src="https://github.com/user-attachments/assets/bf1fd3a3-5bc1-444a-84db-de9cffaee718" />

- To view the DRC errors/ violations flagged for an area:

<img width="1280" height="768" alt="image" src="https://github.com/user-attachments/assets/74e9736a-50a8-4387-8f04-9469a730d6c6" />

Now have a look on the internal layers inside a metal (m3.5)

<img width="1437" height="899" alt="image" src="https://github.com/user-attachments/assets/3e6fae21-a75f-4012-b942-bf2e8eb2f9a6" />





















