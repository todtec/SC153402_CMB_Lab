# Bioinformatics I: Introduction to Sequence Databases and Basic Analysis Tools

## Laboratory Manual for Cell and Molecular Biology Course

---

## ข้อมูลเบื้องต้นเกี่ยวกับปฏิบัติการ

**รหัสปฏิบัติการ:** BioInfo-Lab-01  
**ระยะเวลา:** 3 ชั่วโมง  
**ลักษณะการทำงาน:** Individual/Pair work  
**ข้อกำหนดเบื้องต้น:** ความรู้พื้นฐานเกี่ยวกับ central dogma, DNA structure, และ protein synthesis

---

## จุดประสงค์การเรียนรู้ (Learning Objectives)

เมื่อสิ้นสุดปฏิบัติการนี้ นักศึกษาจะสามารถ:

1. อธิบายความสำคัญของฐานข้อมูลลำดับนิวคลีโอไทด์และโปรตีนต่อการวิจัยทาง molecular biology ได้อย่างมีเหตุผล
2. เข้าถึงและสืบค้นข้อมูลจาก NCBI databases (GenBank, Protein Database) ได้อย่างมีประสิทธิภาพและถูกต้อง
3. วิเคราะห์และตีความข้อมูล sequence annotation ที่ปรากฏใน GenBank record ได้อย่างเป็นระบบ
4. ประยุกต์ใช้เครื่องมือพื้นฐานในการวิเคราะห์คุณสมบัติของลำดับ nucleotide และ amino acid เพื่อการออกแบบการทดลองได้

---

## ส่วนที่ 1: เนื้อหาพื้นฐานทางทฤษฎี

### 1.1 Introduction to Bioinformatics

Bioinformatics เป็นสาขาวิชาสหวิทยาการที่บูรณาการความรู้ทางชีววิทยาระดับโมเลกุล วิทยาการคอมพิวเตอร์ สถิติศาสตร์ และคณิตศาสตร์ เข้าด้วยกัน เพื่อวิเคราะห์และตีความข้อมูลชีววิทยาจำนวนมหาศาล (Lesk, 2019) การพัฒนาของเทคโนโลยี DNA sequencing โดยเฉพาะ Next-Generation Sequencing (NGS) ได้ทำให้เกิดการสะสมข้อมูลลำดับพันธุกรรมอย่างรวดเร็ว จำเป็นต้องอาศัยเครื่องมือและวิธีการทาง computational ในการจัดการและวิเคราะห์ข้อมูลเหล่านี้

### 1.2 Biological Sequence Databases: Architecture and Significance

#### 1.2.1 ประเภทของฐานข้อมูลลำดับพันธุกรรม

ฐานข้อมูลลำดับชีววิทยาสามารถจำแนกได้เป็นสองประเภทหลัก:

**Primary Databases** เป็นฐานข้อมูลที่เก็บข้อมูลลำดับดิบที่ได้จากการทดลองโดยตรง ได้แก่:
- **GenBank** (National Center for Biotechnology Information, NCBI, USA)
- **EMBL** (European Molecular Biology Laboratory, Europe)
- **DDBJ** (DNA Data Bank of Japan, Japan)

ฐานข้อมูลทั้งสามนี้ทำงานร่วมกันภายใต้ International Nucleotide Sequence Database Collaboration (INSDC) โดยมีการแลกเปลี่ยนข้อมูลระหว่างกันเป็นประจำเพื่อให้แน่ใจว่าข้อมูลมีความสมบูรณ์และเป็นปัจจุบัน

**Secondary Databases** เป็นฐานข้อมูลที่ผ่านการคัดกรอง วิเคราะห์ และเพิ่มคุณค่าจากข้อมูลใน primary databases ได้แก่:
- **UniProt** (Universal Protein Resource): รวบรวมข้อมูลลำดับโปรตีนและ functional annotation
- **Pfam**: เก็บข้อมูล protein families และ domains
- **RefSeq**: ข้อมูลลำดับอ้างอิงที่ผ่านการตรวจสอบคุณภาพ (curated sequences)

#### 1.2.2 GenBank Record Structure

GenBank record ประกอบด้วยส่วนสำคัญดังนี้:

- **LOCUS**: ข้อมูลพื้นฐานเกี่ยวกับลำดับ ได้แก่ ชื่อ ความยาว ประเภทของโมเลกุล และวันที่
- **DEFINITION**: คำอธิบายสั้น ๆ เกี่ยวกับลำดับ
- **ACCESSION**: หมายเลขอ้างอิง (accession number) ที่ไม่ซ้ำกัน ใช้ในการอ้างอิงและสืบค้น
- **FEATURES**: ตารางแสดงลักษณะทางชีววิทยาที่สำคัญ เช่น CDS (coding sequence), mRNA, exon, intron, regulatory elements
- **ORIGIN**: ลำดับนิวคลีโอไทด์จริง

### 1.3 Fundamental Concepts in Sequence Analysis

#### 1.3.1 FASTA Format

FASTA format เป็นรูปแบบมาตรฐานในการจัดเก็บและแลกเปลี่ยนข้อมูลลำดับชีววิทยา ประกอบด้วย:
- **Header line**: เริ่มต้นด้วยเครื่องหมาย `>` ตามด้วยชื่อหรือรหัสของลำดับ
- **Sequence lines**: ลำดับนิวคลีโอไทด์หรือกรดอะมิโน โดยทั่วไปจัดเรียงเป็นบรรทัดละ 60-80 ตัวอักษร

ตัวอย่าง:
```
>NM_000518.5 Homo sapiens hemoglobin subunit beta (HBB), mRNA
ACATTTGCTTCTGACACAACTGTGTTCACTAGCAACCTCAAACAGACACCATGGTGCATCTGACTCCTG
AGGAGAAGTCTGCCGTTACTGCCCTGTGGGGCAAGGTGAACGTGGATGAAGTTGGTGGTGAGGCCCTGG
```

#### 1.3.2 Nucleotide Sequence Characteristics

**GC Content**: สัดส่วนของ guanine และ cytosine ในลำดับ DNA คำนวณจากสูตร:

$$\text{GC Content (\%)} = \frac{\text{G + C}}{\text{A + T + G + C}} \times 100$$

GC content มีความสำคัญต่อ:
- Thermal stability ของ DNA (GC pairs มีพันธะไฮโดรเจน 3 พันธะ เทียบกับ AT pairs ที่มี 2 พันธะ)
- Melting temperature (Tm) ในการออกแบบ PCR primers
- Chromatin structure และ gene expression regulation

**Open Reading Frame (ORF)**: ลำดับนิวคลีโอไทด์ระหว่าง start codon (โดยทั่วไปคือ ATG) และ stop codon (TAA, TAG, TGA) ที่สามารถแปลเป็นโปรตีนได้ DNA strand แต่ละเส้นมี reading frames ได้ 3 frames การวิเคราะห์ทั้ง 6 reading frames (3 frames x 2 strands) จำเป็นต่อการระบุ coding sequences

#### 1.3.3 Protein Sequence Properties

**Molecular Weight (MW)**: คำนวณจากผลรวมของ molecular weights ของกรดอะมิโนทั้งหมด หักด้วย molecular weight ของ water molecules ที่ถูกปลดปล่อยระหว่าง peptide bond formation

**Theoretical Isoelectric Point (pI)**: ค่า pH ที่โปรตีนมี net charge เป็นศูนย์ ขึ้นอยู่กับองค์ประกอบของกรดอะมิโนที่มีกลุ่ม ionizable คุณสมบัตินี้มีความสำคัญต่อ:
- Isoelectric focusing (IEF)
- Ion exchange chromatography
- Protein solubility และ crystallization

**GRAVY Score** (Grand Average of Hydropathicity): ค่าเฉลี่ยของ hydropathy values ของกรดอะมิโนทั้งหมดในโปรตีน (Kyte & Doolittle, 1982) ค่า GRAVY ที่เป็นบวกบ่งชี้ว่าโปรตีนมีลักษณะ hydrophobic ในขณะที่ค่าลบบ่งชี้ความเป็น hydrophilic

**Instability Index**: พารามิเตอร์ที่ทำนายความเสถียรของโปรตีนใน vitro โดยโปรตีนที่มีค่า instability index มากกว่า 40 ถือว่าไม่เสถียร (Guruprasad et al., 1990)

---

## ส่วนที่ 2: Hands-on Laboratory Exercises

### Exercise 2.1: Exploring NCBI Portal and GenBank Database

#### วัตถุประสงค์
เพื่อให้นักศึกษาเรียนรู้การใช้งาน NCBI portal และเข้าใจโครงสร้างของ GenBank record

#### อุปกรณ์ที่จำเป็น
- เครื่องคอมพิวเตอร์ที่เชื่อมต่ออินเทอร์เน็ต
- Web browser (แนะนำ Google Chrome, Firefox, หรือ Safari)
- โปรแกรม text editor สำหรับบันทึกข้อมูล (Notepad, TextEdit, หรือ gedit)

#### ขั้นตอนการปฏิบัติ

**ขั้นตอนที่ 1: การเข้าถึง NCBI และทำความเข้าใจ interface**

1.1 เปิด web browser และเข้าสู่เว็บไซต์ NCBI: https://www.ncbi.nlm.nih.gov

1.2 สังเกต components หลักของ homepage:
   - Search box สำหรับการค้นหาข้ามฐานข้อมูล
   - เมนู "Resources" ที่แสดงฐานข้อมูลต่าง ๆ
   - Popular resources: PubMed, GenBank, Gene, Protein

1.3 คลิกที่ dropdown menu ข้าง search box เพื่อดูรายการฐานข้อมูลทั้งหมด

**ขั้นตอนที่ 2: การค้นหา gene sequence**

2.1 ในช่อง search box ให้พิมพ์: `human hemoglobin beta`

2.2 เลือก database เป็น "Gene" จาก dropdown menu

2.3 คลิกปุ่ม "Search" และสังเกตผลลัพธ์ที่ได้

2.4 เลือก gene record ที่มีชื่อว่า "HBB hemoglobin subunit beta [Homo sapiens]"

2.5 ศึกษาข้อมูลใน Gene record:
   - Gene ID (Official gene symbol)
   - Genomic context (chromosome location)
   - Gene type และ description
   - Expression data (if available)

**ขั้นตอนที่ 3: การเข้าถึง nucleotide sequence จาก GenBank**

3.1 ภายใน Gene record ให้เลื่อนลงไปที่ส่วน "Genomic regions, transcripts, and products"

3.2 คลิกที่ mRNA accession number (เช่น NM_000518.5)

3.3 วิเคราะห์ GenBank record ที่ปรากฏ:

   **ส่วน LOCUS:**
   - ความยาวของ mRNA (length in bp)
   - ประเภทโมเลกุล (mRNA)
   - Division code (PRI = primate)
   - Modification date

   **ส่วน DEFINITION:**
   - ชื่อเต็มของ gene และ species

   **ส่วน ACCESSION:**
   - Accession number และ version

   **ส่วน FEATURES:**
   - source: ข้อมูลเกี่ยวกับ organism
   - gene: gene symbol และ locus
   - CDS: coding sequence พร้อม coordinates
   - exon: exon boundaries

3.4 บันทึกข้อมูลต่อไปนี้:
   - Accession number พร้อม version
   - ความยาวของ mRNA
   - จำนวน exons
   - ความยาวของ CDS (จำนวน nucleotides)

**ขั้นตอนที่ 4: การดาวน์โหลดลำดับในรูปแบบ FASTA**

4.1 ที่ด้านบนของหน้า GenBank record คลิกที่ "Send to:"

4.2 เลือก "Complete Record"

4.3 เลือก "File" เป็น destination

4.4 เลือก Format เป็น "FASTA"

4.5 คลิก "Create File" เพื่อดาวน์โหลด

4.6 เปิดไฟล์ที่ดาวน์โหลดด้วย text editor และสังเกตโครงสร้างของ FASTA format

**ขั้นตอนที่ 5: การเปรียบเทียบ genomic DNA กับ mRNA sequence**

5.1 กลับไปที่ Gene record ของ HBB

5.2 ในส่วน "Genomic regions, transcripts, and products" คลิกที่ genomic sequence link (NC_000011.10)

5.3 สังเกตความแตกต่างระหว่าง genomic sequence กับ mRNA sequence:
   - Genomic sequence มี introns
   - mRNA sequence แสดงเฉพาะ exons ที่ต่อกัน (spliced)

5.4 บันทึกข้อสังเกตเกี่ยวกับความแตกต่างระหว่าง genomic organization กับ mature mRNA

---

### Exercise 2.2: Nucleotide Sequence Analysis Using NCBI ORF Finder

#### วัตถุประสงค์
เพื่อฝึกทักษะการระบุ open reading frames และเข้าใจความสำคัญของ genetic code และ reading frames

#### ขั้นตอนการปฏิบัติ

**ขั้นตอนที่ 1: การเข้าถึง ORF Finder tool**

1.1 เข้าสู่เว็บไซต์ NCBI ORF Finder: https://www.ncbi.nlm.nih.gov/orffinder/

1.2 ศึกษา interface และ parameters ที่สามารถปรับได้:
   - Genetic code (standard code = 1)
   - Minimal ORF length
   - Start codon to use (ATG only หรือ alternative start codons)

**ขั้นตอนที่ 2: การวิเคราะห์ ORFs ของ HBB mRNA**

2.1 Copy nucleotide sequence ของ HBB mRNA จาก GenBank (หรือจากไฟล์ FASTA ที่ดาวน์โหลด)

2.2 Paste ลำดับลงใน input box ของ ORF Finder

2.3 ตั้งค่า parameters:
   - Genetic Code: 1 (Standard)
   - Minimal ORF length: 75 nucleotides
   - Start codon: ATG only

2.4 คลิก "Submit" และรอผลลัพธ์

**ขั้นตอนที่ 3: การตีความผลลัพธ์**

3.1 สังเกต graphical representation ที่แสดง:
   - ORFs ในแต่ละ reading frame (6 frames total)
   - ความยาวของแต่ละ ORF (แสดงเป็นแถบสี)
   - Strand direction (+ และ -)

3.2 คลิกที่ ORF ที่ยาวที่สุด (โดยปกติจะเป็น actual coding sequence)

3.3 บันทึกข้อมูล:
   - Reading frame ของ actual CDS
   - Start position และ stop position
   - ความยาวของ ORF (ในหน่วย nucleotides และ amino acids)

3.4 คลิกที่ปุ่ม "Protein" เพื่อดู amino acid sequence ที่แปลได้

**ขั้นตอนที่ 4: การคำนวณ GC content**

4.1 นับจำนวน G และ C bases ในลำดับ (อาจใช้ text editor ที่มี search function)

4.2 คำนวณ GC content ตามสูตร:

$$\text{GC\%} = \frac{(\text{จำนวน G} + \text{จำนวน C})}{\text{ความยาวรวมของลำดับ}} \times 100$$

4.3 ทางเลือกอื่น: ใช้ online GC calculator:
   - เข้าไปที่ https://www.biologicscorp.com/tools/GCContent/
   - Paste nucleotide sequence
   - คลิก "Calculate"

4.4 บันทึก GC content และอภิปรายความหมายทางชีววิทยา:
   - เปรียบเทียบกับ genomic average GC content ของมนุษย์ (~41%)
   - ความสัมพันธ์กับ thermal stability

---

### Exercise 2.3: Protein Sequence Analysis Using ExPASy ProtParam

#### วัตถุประสงค์
เพื่อวิเคราะห์คุณสมบัติทางกายภาพและเคมีของโปรตีน และเข้าใจการประยุกต์ใช้ข้อมูลในการออกแบบการทดลอง

#### ขั้นตอนการปฏิบัติ

**ขั้นตอนที่ 1: การเตรียม amino acid sequence**

1.1 จาก ORF Finder ในขั้นตอนก่อนหน้า ให้ copy amino acid sequence ของ HBB

1.2 หรือเข้าไปที่ NCBI Protein database และค้นหา "human hemoglobin beta"

1.3 เลือก protein record (เช่น NP_000509.1)

1.4 ดาวน์โหลด sequence ในรูปแบบ FASTA

**ขั้นตอนที่ 2: การใช้งาน ProtParam tool**

2.1 เข้าสู่เว็บไซต์ ExPASy ProtParam: https://web.expasy.org/protparam/

2.2 Paste amino acid sequence ลงใน input box (อาจเป็น FASTA format หรือ plain sequence)

2.3 คลิก "Compute parameters"

**ขั้นตอนที่ 3: การวิเคราะห์ผลลัพธ์**

วิเคราะห์และบันทึกพารามิเตอร์ต่อไปนี้พร้อมความหมาย:

**3.1 Physical Parameters:**
- **Number of amino acids**: จำนวนกรดอะมิโนรวม
- **Molecular weight**: น้ำหนักโมเลกุล (Daltons) ใช้ในการ:
  - การคำนวณความเข้มข้นของโปรตีน
  - การเลือกขนาด pore ของ gel ใน SDS-PAGE
  - การประเมินผลการทำ chromatography

**3.2 Chemical Composition:**
- **Amino acid composition**: สัดส่วนของกรดอะมิโนแต่ละชนิด (%)
  - สังเกตกรดอะมิโนที่พบมากที่สุดและน้อยที่สุด
  - เชื่อมโยงกับโครงสร้างและหน้าที่ของโปรตีน
  
- **Atomic composition**: จำนวนอะตอมของธาตุต่าง ๆ (C, H, N, O, S)

**3.3 Theoretical pI:**
- ค่า pH ที่โปรตีนมี net charge = 0
- การประยุกต์ใช้:
  - Isoelectric focusing (IEF)
  - Ion exchange chromatography: เลือก resin type (anion/cation exchanger)
  - ทำนาย solubility ที่ pH ต่าง ๆ
  
บันทึก: โปรตีนมี solubility ต่ำที่สุดเมื่ออยู่ที่ pH = pI

**3.4 Extinction Coefficient:**
- ค่าสัมประสิทธิ์การดูดกลืนแสงที่ 280 nm
- คำนวณจากเนื้อหาของ Trp, Tyr, และ Cys residues
- การประยุกต์ใช้:
  - คำนวณความเข้มข้นของโปรตีนจากการวัด absorbance
  - ใช้สูตร: C (M) = A₂₈₀ / ε (M⁻¹cm⁻¹)

**3.5 Instability Index:**
- ทำนายความเสถียรของโปรตีนใน vitro
- การตีความ:
  - II < 40: โปรตีนมีความเสถียร (stable)
  - II > 40: โปรตีนไม่เสถียร (unstable)
- มีประโยชน์ในการวางแผนการทำ protein expression และ purification

**3.6 Aliphatic Index:**
- ความอุดมสมบูรณ์ของ aliphatic side chains (Ala, Val, Ile, Leu)
- ค่าที่สูงบ่งชี้ thermal stability ที่ดี
- มีความสำคัญในการศึกษา thermophilic proteins

**3.7 GRAVY (Grand Average of Hydropathicity):**
- ค่าเฉลี่ยของ hydropathy scores ทุก amino acid residues
- การตีความ:
  - GRAVY > 0: โปรตีนมีลักษณะ hydrophobic (membrane proteins)
  - GRAVY < 0: โปรตีนมีลักษณะ hydrophilic (soluble proteins)

**ขั้นตอนที่ 4: การวิเคราะห์เชิงลึก**

4.1 คลิกที่ลิงก์ "Amino acid scale" ภายในผลลัพธ์

4.2 เลือก scale: "Kyte & Doolittle" (hydropathy scale)

4.3 สังเกต hydropathy plot:
   - Peak ที่เป็นบวก: hydrophobic regions
   - Valley ที่เป็นลบ: hydrophilic regions
   - ความยาวของ hydrophobic stretches (อาจบ่งชี้ transmembrane domains)

4.4 สำหรับ hemoglobin beta: สังเกตว่ามี hydrophobic regions สั้น ๆ กระจายอยู่ สอดคล้องกับการเป็น globular protein ที่ละลายน้ำได้

---

## ส่วนที่ 3: แบบฝึกหัดและการประยุกต์ใช้

### Exercise Set 3.1: Guided Exercise - Gene and Protein Analysis

**คำสั่ง:** เลือกศึกษา gene หนึ่งจากรายการต่อไปนี้ และทำการวิเคราะห์ตามขั้นตอนที่กำหนด

**รายการ Genes:**
1. TP53 (tumor protein p53) - tumor suppressor gene
2. BRCA1 (breast cancer 1) - DNA repair gene
3. INS (insulin) - metabolic hormone gene
4. CFTR (cystic fibrosis transmembrane conductance regulator)
5. DMD (dystrophin) - muscle structure gene

---

#### ส่วนที่ A: Nucleotide Sequence Analysis

**A1. การค้นหาและบันทึกข้อมูลพื้นฐาน**

ให้ทำการค้นหา gene ที่เลือกใน NCBI Gene database และบันทึกข้อมูลต่อไปนี้:

| พารามิเตอร์ | ข้อมูล |
|------------|--------|
| Gene Symbol | |
| Gene ID | |
| Official Full Name | |
| Organism | |
| Chromosome Location | |
| Gene Type | |

**A2. mRNA Sequence Analysis**

เข้าถึง representative mRNA record (RefSeq: NM_xxxxxx) และบันทึก:

| พารามิเตอร์ | ค่าที่วัดได้ |
|------------|-------------|
| Accession Number (with version) | |
| mRNA Length (bp) | |
| Number of Exons | |
| CDS Length (bp) | |
| 5' UTR Length (bp) | |
| 3' UTR Length (bp) | |
| GC Content (%) | |

**คำถามวิเคราะห์:**

1. จากข้อมูล GC content ที่คำนวณได้ เปรียบเทียบกับค่าเฉลี่ย genome-wide GC content ของมนุษย์ (~41%) Gene นี้มี GC content สูงหรือต่ำกว่าค่าเฉลี่ย? อภิปรายความหมายที่เป็นไปได้

2. คำนวณ coding efficiency:
   $$\text{Coding Efficiency} = \frac{\text{CDS Length}}{\text{mRNA Length}} \times 100\%$$
   
   ค่าที่ได้บ่งชี้อะไรเกี่ยวกับ regulatory regions และ post-transcriptional regulation?

**A3. ORF Analysis**

ใช้ NCBI ORF Finder วิเคราะห์ mRNA sequence:

| พารามิเตอร์ | ผลลัพธ์ |
|------------|---------|
| จำนวน ORFs ที่พบ (length ≥ 75 nt) | |
| Longest ORF - Reading Frame | |
| Longest ORF - Start Position | |
| Longest ORF - Stop Position | |
| Longest ORF - Length (aa) | |
| จำนวน amino acids ที่คาดการณ์จาก CDS annotation | |

**คำถามวิเคราะห์:**

3. ORF ที่ยาวที่สุดที่พบจาก ORF Finder ตรงกับ CDS ที่ annotate ไว้ใน GenBank หรือไม่? หากไม่ตรง อธิบายสาเหตุที่เป็นไปได้

4. มี alternative ORFs ที่มีความยาวใกล้เคียงกับ main ORF หรือไม่? อภิปรายความเป็นไปได้ของ alternative translation initiation sites

---

#### ส่วนที่ B: Protein Sequence Analysis

**B1. การเข้าถึง Protein Sequence**

ค้นหา protein product ที่สอดคล้องกับ mRNA ใน NCBI Protein database (RefSeq: NP_xxxxxx)

| พารามิเตอร์ | ข้อมูล |
|------------|--------|
| Protein Accession Number | |
| Protein Name | |
| Number of Amino Acids | |

**B2. ProtParam Analysis**

ใช้ ExPASy ProtParam วิเคราะห์ protein sequence และบันทึกผลลัพธ์:

| Physical-Chemical Parameter | Value | Interpretation/Application |
|----------------------------|-------|---------------------------|
| Molecular Weight (Da) | | |
| Theoretical pI | | |
| Total number of negatively charged residues (Asp + Glu) | | |
| Total number of positively charged residues (Arg + Lys) | | |
| Extinction coefficient at 280 nm (M⁻¹cm⁻¹) | | |
| Instability Index | | Stable (< 40) / Unstable (> 40) |
| Aliphatic Index | | |
| GRAVY | | Hydrophobic (> 0) / Hydrophilic (< 0) |

**B3. Amino Acid Composition Analysis**

จาก amino acid composition table ให้ระบุ:

| Category | Amino Acids (3-letter code) | Percentage |
|----------|----------------------------|------------|
| Most abundant amino acid | | |
| Second most abundant | | |
| Least abundant (non-zero) | | |
| Aromatic amino acids (Phe, Tyr, Trp) | | |
| Hydrophobic amino acids (Ala, Val, Ile, Leu, Met, Phe, Trp, Pro) | | |

**คำถามวิเคราะห์:**

5. จากค่า theoretical pI หากต้องการทำ ion exchange chromatography เพื่อ purify โปรตีนนี้ที่ pH 7.4:
   - โปรตีนจะมี net charge เป็นบวกหรือลบ?
   - ควรเลือกใช้ anion exchanger หรือ cation exchanger? อธิบาย

6. หากต้องการคำนวณความเข้มข้นของ purified protein โดยการวัด absorbance ที่ 280 nm และได้ค่า A₂₈₀ = 0.5 (ใช้ cuvette 1 cm path length) ความเข้มข้นของโปรตีนเป็นเท่าใด (หน่วย mg/mL)?
   
   *สูตร:* 
   $$C (\text{mg/mL}) = \frac{A_{280} \times \text{MW (Da)}}{\varepsilon \text{ (M}^{-1}\text{cm}^{-1}\text{)}}$$
   
   (หมายเหตุ: 1 M = 1 mol/L; ต้องแปลงหน่วยอย่างเหมาะสม)

7. จากค่า instability index และ GRAVY score:
   - คาดการณ์ว่าโปรตีนนี้จะ express และ purify ได้ง่ายหรือยาก?
   - โปรตีนนี้น่าจะเป็น membrane protein, cytoplasmic protein, หรือ secreted protein? อ้างอิงข้อมูลจาก GRAVY score ประกอบ

8. วิเคราะห์ hydropathy plot (Kyte & Doolittle scale):
   - มี hydrophobic stretches ที่ยาวพอที่จะเป็น transmembrane domain (~ 20-25 residues) หรือไม่?
   - สังเกตลวดลายของ hydrophobic/hydrophilic regions และเชื่อมโยงกับโครงสร้างและหน้าที่ของโปรตีน

---

### Exercise Set 3.2: Problem-Based Exercise - Unknown Sequence Identification

**Scenario:** นักวิจัยได้รับ DNA sequence จากการทำ PCR แต่ไม่ทราบว่าเป็น gene อะไร ท่านในฐานะนักชีววิทยาระดับโมเลกุลจะต้องใช้เครื่องมือ bioinformatics ในการระบุ identity และวิเคราะห์คุณสมบัติของลำดับนี้

**Unknown Sequence:**

```
>Unknown_Sequence
ATGGGTCTGAGCGGTGGCGCCGCCGCCAAGCGGCGGCCCCCCGCGCCGCTGCTGCTGCT
GCTCGGGGCCCTCGGCTGCGCCATGGGGGAGCTGCCCCCCAGCGGTTTCTTTGACGGGG
ACAAGGCCTTCCTGCAGAAGGAGAATTATGCTGTTCCCGTCCATGCCTTGACCCGGGAG
AACGGTGAGCTGCTGATCGACAAGAACATGGAGAAGGACCCCGCGTTCCAGAAGTACTT
CCAGTCCACGGACTACTACGCCAACGGACTGAAGGACTACCTGGAGCGCAAGGAGGCCA
TCAAGGGCAAGAACGTGCTGCCCATCTTCGACACGAAGGACGAGGACGACGGCAAGGGC
TTCATCAAGGAGATGGTGATCAAGGGTTTCAAGGTGTGGGAGAAGTACGAGGACGGCGG
CATTGTGACCATTGAGCAGGACGGCAGCTTCATCTACAAGGTGAAGTTCATCGGCACCAA
CTTCCCCCCGGATGGCCCGGTGATGCAGAAGAAGACCATGGGCTGGGAGGCCTCCACCG
AGCGCCTGTACCCGCGCGATGGCGTGCTGAAGGGCGAGATCAAGCAGAGGCTGAAGCTG
AAGGACGGCGGCCACTACCTGGTGGAGTTCAAGACCATCTACATGGCCAAGAAGCCGGT
GCAGCTGCCCGGCTACTACTACGTGGACTCCCGCCTGGAGCGCGGCAGCTTCCACCTCT
GCTCCATGGTGATGATGGGCGGCAGCTTGACACCGGGCTGGGGAGAGGTGTACCAGTCG
GACATGACCATGAGGGTGAATACCGCCGCCCCGGAGGCCGCCTGA
```

#### Tasks:

**Task 1: Basic Sequence Characterization**

1. ใช้ NCBI BLAST (BLASTn - nucleotide BLAST) ค้นหา identity ของลำดับนี้
   - เข้าสู่ https://blast.ncbi.nlm.nih.gov/Blast.cgi?PROGRAM=blastn&PAGE_TYPE=BlastSearch
   - Paste sequence ลงใน input box
   - เลือก database: "Nucleotide collection (nr/nt)"
   - คลิก "BLAST"

2. จากผลลัพธ์ BLAST บันทึกข้อมูล hit อันดับ 1 (best match):

| Parameter | Value |
|-----------|-------|
| Gene Name | |
| Organism | |
| Accession Number | |
| Query Coverage (%) | |
| Percent Identity (%) | |
| E-value | |

**คำถามวิเคราะห์:**

9. E-value มีความหมายว่าอะไร? ค่า E-value ที่ได้บ่งชี้ว่าผลลัพธ์นี้มีความน่าเชื่อถือหรือไม่?

10. Query coverage และ percent identity ที่ได้บ่งบอกอะไรเกี่ยวกับความสัมพันธ์ระหว่าง unknown sequence กับ hit ที่ดีที่สุด?

**Task 2: Functional Analysis**

3. ค้นหา Gene record ของ gene ที่ระบุได้จาก BLAST
   
4. อ่านข้อมูล functional annotation และบันทึก:
   - Gene function (biological role)
   - Pathway involvement (ถ้ามี)
   - Tissue/cell type expression
   - Clinical significance (ถ้ามี)

**Task 3: Sequence Properties Analysis**

5. คำนวณ/วิเคราะห์คุณสมบัติต่อไปนี้:

| Property | Value | Method/Tool Used |
|----------|-------|-----------------|
| Sequence Length (bp) | | Direct count |
| GC Content (%) | | GC calculator หรือ manual calculation |
| Number of ORFs (length ≥ 75 nt) | | NCBI ORF Finder |
| Longest ORF Length (aa) | | NCBI ORF Finder |
| Predicted Protein MW (Da) | | ExPASy ProtParam |
| Predicted Protein pI | | ExPASy ProtParam |

**Task 4: Comparative Analysis**

6. ทำ BLASTn เพื่อหา homologous sequences จากอย่างน้อย 3 organisms ที่แตกต่างกัน

7. เปรียบเทียบ percent identity ระหว่าง organisms:

| Organism | Common Name | Percent Identity (%) | Evolutionary Distance from Reference |
|----------|-------------|---------------------|-------------------------------------|
| | | | |
| | | | |
| | | | |

**คำถามวิเคราะห์:**

11. จากการเปรียบเทียบ percent identity ข้าม species อธิบายความสัมพันธ์เชิงวิวัฒนาการ (evolutionary conservation) ของ gene นี้

12. Conservation ระดับสูงบ่งบอกอะไรเกี่ยวกับความสำคัญทางชีววิทยาของ gene นี้?

---

### Exercise Set 3.3: Application Questions

**คำถามเชิงประยุกต์และการคิดวิเคราะห์:**

13. สมมติว่าท่านต้องการออกแบบ primers สำหรับ PCR amplification ของ gene ที่ท่านศึกษา:
    - ข้อมูล GC content มีความสำคัญอย่างไร?
    - ควรเลือกบริเวณใดของ gene เป็น primer binding sites (5' UTR, CDS, 3' UTR)? เพราะเหตุใด?
    - หากต้องการ amplify เฉพาะ coding region ควรออกแบบ primers อย่างไร?

14. ในการทำ recombinant protein expression:
    - ข้อมูล codon usage มีความสำคัญอย่างไร (เชื่อมโยงกับ GC content)?
    - ค่า pI ของโปรตีนมีผลต่อการเลือก purification strategy อย่างไร?
    - Instability index สามารถช่วยทำนายปัญหาในการ express protein ได้หรือไม่?

15. พิจารณาสถานการณ์: นักวิจัยพบว่าโปรตีนที่ purify ได้มีแนวโน้มเกิด precipitation ที่ pH 7.0
    - การรู้ค่า theoretical pI ช่วยอธิบายปรากฏการณ์นี้ได้อย่างไร?
    - ควรปรับ pH ของ buffer ไปในทิศทางใด (สูงขึ้นหรือต่ำลง) เพื่อเพิ่ม solubility?

16. เปรียบเทียบข้อดีข้อเสียของการใช้:
    - Primary databases (GenBank) vs. Secondary databases (UniProt)
    - Web-based tools vs. Standalone software สำหรับ sequence analysis

17. อธิบายความสำคัญของ accession number และ version number ในการอ้างอิงข้อมูลทางวิทยาศาสตร์

18. หากพบว่าโปรตีนที่ศึกษามี GRAVY score เป็นค่าบวกสูง (เช่น +1.2) และมี prolonged hydrophobic stretches จาก hydropathy plot:
    - โปรตีนนี้น่าจะ localize ที่ส่วนใดของเซลล์?
    - มีข้อควรพิจารณาพิเศษอะไรในการทำ expression และ purification?

---

## ส่วนที่ 4: การส่งรายงานและเกณฑ์การประเมินผล

### 4.1 รูปแบบการส่งรายงาน

นักศึกษาจะต้องจัดทำและส่งรายงานปฏิบัติการในรูปแบบ PDF หรือ Word document ประกอบด้วยส่วนต่อไปนี้:

**1. Title Page**
   - ชื่อปฏิบัติการ
   - รหัสวิชาและชื่อรายวิชา
   - ชื่อ-นามสกุล และรหัสนักศึกษา
   - วันที่ทำปฏิบัติการ
   - ชื่ออาจารย์ผู้สอน

**2. Introduction**
   - วัตถุประสงค์ของการทดลอง (สรุปย่อ)
   - ความสำคัญของ bioinformatics และ sequence databases

**3. Materials and Methods**
   - รายชื่อเครื่องมือและฐานข้อมูลที่ใช้ (NCBI, ORF Finder, ProtParam)
   - สรุปขั้นตอนการทำงาน (ไม่ต้องระบุทุกขั้นตอนละเอียด)

**4. Results**
   - Exercise Set 3.1: แสดงตารางและข้อมูลที่บันทึกครบถ้วน
   - Exercise Set 3.2: แสดงผลลัพธ์ BLAST พร้อม screenshots สำคัญ
   - รวม screenshots หรือ figures ที่เกี่ยวข้อง (GenBank records, ORF Finder output, ProtParam results, Hydropathy plot) พร้อม figure legends

**5. Discussion**
   - ตอบคำถามวิเคราะห์ทั้งหมด (คำถามที่ 1-18) อย่างละเอียดและมีเหตุผล
   - เชื่อมโยงผลที่ได้กับความรู้ทางทฤษฎีและการประยุกต์ใช้จริง
   - อภิปรายข้อจำกัดของเครื่องมือที่ใช้ (ถ้ามี)

**6. Conclusions**
   - สรุปสิ่งที่เรียนรู้จากปฏิบัติการนี้
   - ความสามารถที่ได้รับจากการฝึกปฏิบัติ

**7. References**
   - อ้างอิงแหล่งข้อมูลที่ใช้ (GenBank records, publications, web tools) ในรูปแบบมาตรฐาน

### 4.2 เกณฑ์การประเมินผล (รวม 10 คะแนน)

| หมวดการประเมิน | รายละเอียด | คะแนน |
|----------------|-----------|-------|
| **1. การเข้าร่วมและการปฏิบัติ** | - เข้าร่วมปฏิบัติการตรงเวลา<br>- ปฏิบัติตามขั้นตอนอย่างเป็นระบบ<br>- มีส่วนร่วมในกิจกรรม | 2 |
| **2. ความถูกต้องของข้อมูล (Exercise 3.1)** | - ความครบถ้วนของตารางข้อมูล<br>- ความแม่นยำของการบันทึก parameters<br>- การนำเสนอผลลัพธ์อย่างเป็นระบบ | 2 |
| **3. การวิเคราะห์และแก้ปัญหา (Exercise 3.2)** | - ความถูกต้องในการใช้ BLAST<br>- การระบุ gene identity<br>- ความสมบูรณ์ของ comparative analysis | 2 |
| **4. คำตอบคำถามวิเคราะห์** | - ความถูกต้องของคำตอบ (ข้อ 1-18)<br>- ความลึกซึ้งของการวิเคราะห์<br>- การเชื่อมโยงทฤษฎีกับการประยุกต์ใช้<br>- การใช้เหตุผลทางวิทยาศาสตร์ | 3 |
| **5. รูปแบบและการนำเสนอรายงาน** | - ความเป็นระเบียบของรายงาน<br>- การใช้ภาษาทางวิทยาศาสตร์<br>- คุณภาพของ figures และ tables<br>- การอ้างอิง references | 1 |

**หมายเหตุ:** รายงานที่ส่งล่าช้าจะถูกหักคะแนน 10% ต่อวัน

### 4.3 Rubric รายละเอียด

#### การประเมินคำตอบคำถามวิเคราะห์ (3 คะแนน)

**ระดับดีเยี่ยม (2.5-3 คะแนน):**
- ตอบคำถามครบถ้วนทุกข้อ
- แสดงความเข้าใจเชิงลึกและสามารถเชื่อมโยงแนวคิดได้
- ใช้ข้อมูลจากการทดลองสนับสนุนคำตอบอย่างเหมาะสม
- มีการวิเคราะห์เปรียบเทียบและให้เหตุผลทางวิทยาศาสตร์

**ระดับดี (2.0-2.4 คะแนน):**
- ตอบคำถามครบถ้วนส่วนใหญ่
- แสดงความเข้าใจพื้นฐานที่ถูกต้อง
- ใช้ข้อมูลจากการทดลองประกอบคำตอบ
- มีการวิเคราะห์แต่อาจขาดความลึกซึ้ง

**ระดับพอใช้ (1.5-1.9 คะแนน):**
- ตอบคำถามได้บางส่วน
- ความเข้าใจพื้นฐานแต่อาจมีข้อผิดพลาดบางประการ
- การวิเคราะห์ไม่ลึกซึ้ง
- ขาดการเชื่อมโยงระหว่างทฤษฎีกับการปฏิบัติ

**ระดับปรับปรุง (< 1.5 คะแนน):**
- ตอบคำถามไม่ครบถ้วน
- แสดงความเข้าใจที่คลาดเคลื่อนหรือไม่ถูกต้อง
- ขาดการวิเคราะห์เชิงลึก

---

## ส่วนที่ 5: แหล่งข้อมูลเพิ่มเติมและการอ่านเพิ่มเติม

### 5.1 Web Resources และ Tutorials

**NCBI Resources:**
- NCBI Education: https://www.ncbi.nlm.nih.gov/home/learn/
- NCBI Handbook: https://www.ncbi.nlm.nih.gov/books/NBK143764/
- GenBank Overview: https://www.ncbi.nlm.nih.gov/genbank/
- Video tutorials: https://www.youtube.com/user/NCBINLM

**ExPASy Resources:**
- ExPASy Bioinformatics Resource Portal: https://www.expasy.org/
- ProtParam Tool documentation: https://web.expasy.org/protparam/protparam-doc.html
- Swiss-Prot protein database: https://www.uniprot.org/

**Additional Tools:**
- EMBL-EBI Tools: https://www.ebi.ac.uk/services
- EMBOSS Suite: http://emboss.sourceforge.net/
- Sequence Manipulation Suite: http://www.bioinformatics.org/sms2/

### 5.2 คำศัพท์สำคัญและคำจำกัดความ

| คำศัพท์ | คำจำกัดความ |
|---------|-------------|
| **Accession Number** | รหัสอ้างอิงเฉพาะที่ใช้ระบุ sequence record ในฐานข้อมูล ไม่เปลี่ยนแปลงแม้ sequence จะถูกแก้ไข |
| **Annotation** | การเพิ่มข้อมูลเชิงชีววิทยาลงใน sequence record เช่น ตำแหน่งของ genes, regulatory elements, protein domains |
| **CDS (Coding Sequence)** | ส่วนของ nucleotide sequence ที่แปลเป็น amino acids (ไม่รวม introns ใน genomic DNA) |
| **E-value (Expect value)** | ค่าทางสถิติที่บ่งบอกความน่าจะเป็นที่ sequence alignment จะเกิดขึ้นโดยบังเอิญ ยิ่งค่าต่ำยิ่งมีนัยสำคัญ |
| **FASTA format** | รูปแบบมาตรฐานสำหรับจัดเก็บ biological sequences ประกอบด้วย header line (>) และ sequence lines |
| **GenBank** | ฐานข้อมูล nucleotide sequences ของ NCBI ที่เก็บข้อมูล DNA และ RNA sequences จากทุกสิ่งมีชีวิต |
| **Homology** | ความสัมพันธ์ระหว่าง sequences ที่มาจาก common ancestor เดียวกัน แบ่งเป็น orthology และ paralogy |
| **ORF (Open Reading Frame)** | ลำดับระหว่าง start codon และ stop codon ที่สามารถแปลเป็น protein ได้ |
| **RefSeq** | Reference Sequence database ที่เก็บ non-redundant, curated sequences ที่มีคุณภาพสูง |
| **UTR (Untranslated Region)** | บริเวณใน mRNA ที่ไม่ถูกแปลเป็นโปรตีน แบ่งเป็น 5' UTR (upstream ของ start codon) และ 3' UTR (downstream ของ stop codon) |

### 5.3 เอกสารอ้างอิงหลัก

Altschul, S.F., Gish, W., Miller, W., Myers, E.W., & Lipman, D.J. (1990). Basic local alignment search tool. *Journal of Molecular Biology*, 215(3), 403-410. https://doi.org/10.1016/S0022-2836(05)80360-2

Benson, D.A., Cavanaugh, M., Clark, K., Karsch-Mizrachi, I., Lipman, D.J., Ostell, J., & Sayers, E.W. (2013). GenBank. *Nucleic Acids Research*, 41(D1), D36-D42. https://doi.org/10.1093/nar/gks1195

Gasteiger, E., Hoogland, C., Gattiker, A., Duvaud, S., Wilkins, M.R., Appel, R.D., & Bairoch, A. (2005). Protein identification and analysis tools on the ExPASy server. In J.M. Walker (Ed.), *The Proteomics Protocols Handbook* (pp. 571-607). Humana Press. https://doi.org/10.1385/1-59259-890-0:571

Guruprasad, K., Reddy, B.V., & Pandit, M.W. (1990). Correlation between stability of a protein and its dipeptide composition: a novel approach for predicting in vivo stability of a protein from its primary sequence. *Protein Engineering, Design and Selection*, 4(2), 155-161. https://doi.org/10.1093/protein/4.2.155

Kyte, J., & Doolittle, R.F. (1982). A simple method for displaying the hydropathic character of a protein. *Journal of Molecular Biology*, 157(1), 105-132. https://doi.org/10.1016/0022-2836(82)90515-0

Lesk, A.M. (2019). *Introduction to Bioinformatics* (5th ed.). Oxford University Press.

Mount, D.W. (2007). *Bioinformatics: Sequence and Genome Analysis* (2nd ed.). Cold Spring Harbor Laboratory Press.

O'Leary, N.A., Wright, M.W., Brister, J.R., et al. (2016). Reference sequence (RefSeq) database at NCBI: current status, taxonomic expansion, and functional annotation. *Nucleic Acids Research*, 44(D1), D733-D745. https://doi.org/10.1093/nar/gkv1189

The UniProt Consortium. (2023). UniProt: the Universal Protein Knowledgebase in 2023. *Nucleic Acids Research*, 51(D1), D523-D531. https://doi.org/10.1093/nar/gkac1052

---

## ภาคผนวก: คำแนะนำสำหรับอาจารย์ผู้สอน

### A.1 การเตรียมการก่อนสอน

**ด้านเทคนิค:**
1. ทดสอบการเชื่อมต่ออินเทอร์เน็ตของห้องปฏิบัติการล่วงหน้าอย่างน้อย 1 สัปดาห์
2. ตรวจสอบว่าเว็บเบราว์เซอร์ของเครื่องคอมพิวเตอร์ทุกเครื่องสามารถเข้าถึง NCBI และ ExPASy ได้
3. เตรียม backup local copies ของ tutorials และ sample sequences กรณีเว็บไซต์ล่ม
4. ติดตั้งหรือตรวจสอบ text editors ที่เหมาะสม (Notepad++, Sublime Text, หรือ gedit)

**ด้านเนื้อหา:**
1. ทบทวนความรู้พื้นฐานเกี่ยวกับ central dogma และ molecular biology ก่อนเริ่มปฏิบัติการ
2. เตรียม slide presentation สำหรับส่วนบรรยาย (20-25 slides)
3. จัดทำ step-by-step demonstration script พร้อม screenshots
4. เตรียม example genes ที่หลากหลายสำหรับให้นักศึกษาเลือก (พิจารณาความสนใจและ background ของนักศึกษา)

**การจัดการชั้นเรียน:**
1. แบ่งนักศึกษาเป็นกลุ่มล่วงหน้า (ถ้าทำงานเป็นคู่)
2. กำหนด teaching assistant (TA) หรือผู้ช่วยสอน 1 คนต่อนักศึกษา 15-20 คน
3. เตรียม Google Sheets หรือ shared folder สำหรับให้นักศึกษา upload ผลงาน real-time

### A.2 กลยุทธ์การสอน

**สำหรับนักศึกษาที่มีพื้นฐานต่าง ๆ:**

**นักศึกษาที่มีพื้นฐาน Molecular Biology ดี แต่ไม่คุ้นเคยกับ Bioinformatics:**
- เน้นการเชื่อมโยงแนวคิดทาง computational กับความรู้ทาง wet lab ที่มีอยู่
- ยกตัวอย่างการประยุกต์ใช้เครื่องมือ bioinformatics ในการออกแบบการทดลอง
- สร้าง scenario-based learning ที่เกี่ยวข้องกับการวิจัยจริง

**นักศึกษาที่มีทักษะ Computer แต่ขาดพื้นฐาน Biology:**
- เสริมความรู้พื้นฐานทาง molecular biology ก่อนเข้าสู่ hands-on
- ให้เวลาในการทำความเข้าใจ biological context
- เน้นการตีความผลลัพธ์ในบริบททางชีววิทยา

**นักศึกษาที่ขาดพื้นฐานทั้งสองด้าน:**
- จัดให้มี pre-lab reading assignments
- จัดเวลา office hours เพิ่มเติมสำหรับให้คำปรึกษา
- ใช้ peer teaching โดยจับคู่กับนักศึกษาที่มีพื้นฐานดีกว่า

### A.3 การจัดการปัญหาที่อาจเกิดขึ้น

| ปัญหา | สาเหตุที่เป็นไปได้ | แนวทางแก้ไข |
|-------|-------------------|-------------|
| เว็บไซต์ NCBI ช้าหรือเข้าไม่ได้ | Traffic สูง, การบำรุงรักษาระบบ | - ใช้ mirror sites<br>- เตรียม offline data<br>- เลื่อนเวลาปฏิบัติการ |
| นักศึกษาค้นหาข้อมูลไม่เจอ | ใช้ search terms ไม่เหมาะสม | - สอนการใช้ Boolean operators<br>- ให้ตัวอย่าง effective search strategies |
| ผลลัพธ์ ProtParam แปลกประหลาด | Input sequence ผิดพลาด | - ตรวจสอบว่าเป็น protein sequence<br>- ตรวจสอบ FASTA format<br>- ลบ special characters |
| นักศึกษาใช้เวลานานเกินไป | ขาดความชำนาญในการใช้เครื่องมือ | - ให้คำแนะนำเฉพาะบุคคล<br>- จัดทำ quick reference guide<br>- ปรับเวลาตามความเหมาะสม |

### A.4 การขยายเนื้อหาสำหรับนักศึกษาระดับสูง

สำหรับนักศึกษาระดับปริญญาตรีชั้นปีสูงหรือระดับบัณฑิตศึกษา อาจเพิ่มเนื้อหาต่อไปนี้:

1. **Command-line BLAST**: แนะนำการใช้ standalone BLAST สำหรับการวิเคราะห์จำนวนมาก
2. **Batch processing**: การ download และวิเคราะห์ sequences หลายลำดับพร้อมกัน
3. **API access**: การใช้ NCBI E-utilities สำหรับการดึงข้อมูลแบบ programmatic
4. **Advanced protein analysis**: การใช้เครื่องมือทำนาย post-translational modifications, signal peptides, subcellular localization

### A.5 การประเมินผลและ Feedback

**การให้ feedback ที่มีประสิทธิภาพ:**
1. ให้ feedback เป็นระยะ ไม่ใช่แค่ตอนส่งรายงานเท่านั้น
2. เน้น formative assessment ระหว่างปฏิบัติการ
3. ใช้ rubric ที่ชัดเจนและแบ่งปัน criteria กับนักศึกษาตั้งแต่ต้น
4. ให้ positive reinforcement ควบคู่กับ constructive criticism

**ตัวอย่าง feedback comments:**
- *ดีเยี่ยม:* "คำตอบของคุณแสดงให้เห็นความเข้าใจเชิงลึกเกี่ยวกับความสัมพันธ์ระหว่าง pI และการเลือก chromatography method คุณสามารถเชื่อมโยงทฤษฎีกับการปฏิบัติได้ดีมาก"
- *ปรับปรุง:* "การวิเคราะห์ของคุณมีความถูกต้องพื้นฐาน แต่ควรขยายความเกี่ยวกับความหมายทางชีววิทยาของ conservation ที่พบเพิ่มเติม ลองพิจารณาว่า conserved regions เหล่านี้อาจเกี่ยวข้องกับ functional domains ที่สำคัญหรือไม่"

---

## สรุป

ปฏิบัติการนี้ได้ถูกออกแบบเพื่อให้นักศึกษาได้รับประสบการณ์ hands-on ในการใช้เครื่องมือ bioinformatics พื้นฐานที่จำเป็นต่อการศึกษาวิจัยทางชีววิทยาระดับโมเลกุล ผ่านการเรียนรู้แบบ constructivist และ active learning นักศึกษาจะสามารถพัฒนาทักษะการคิดวิเคราะห์ การแก้ปัญหา และการประยุกต์ใช้เทคโนโลยีสารสนเทศในบริบททางชีววิทยา

ความสามารถในการเข้าถึง วิเคราะห์ และตีความข้อมูล sequence จากฐานข้อมูลสาธารณะเป็นทักษะพื้นฐานที่จำเป็นสำหรับนักวิทยาศาสตร์ชีวภาพในยุคปัจจุบัน การฝึกปฏิบัติในห้องเรียนนี้จะเป็นรากฐานสำคัญสำหรับการเรียนรู้ bioinformatics ในระดับที่สูงขึ้นต่อไป

---

**เอกสารประกอบการสอนฉบับนี้จัดทำโดย:** [ชื่ออาจารย์ผู้สอน]  
**สถาบัน:** [ชื่อมหาวิทยาลัย/สถาบัน]  
**วันที่จัดทำ:** [วัน/เดือน/ปี]  
**เวอร์ชัน:** 1.0  

**License:** This educational material is released under Creative Commons Attribution-NonCommercial-ShareAlike 4.0 International License (CC BY-NC-SA 4.0)

---

**สำหรับคำถามหรือข้อเสนอแนะเพิ่มเติม:**  
Email: [อีเมลติดต่อ]  
Office: [ห้องทำงาน]  
Office Hours: [เวลาให้คำปรึกษา]
