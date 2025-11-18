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

## LAB-03 Introduction to Sky130 basic layers layout and LEF using inverter


