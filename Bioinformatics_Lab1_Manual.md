# Bioinformatics I: Introduction to Sequence Databases and Basic Analysis Tools

## Laboratory Manual for Cell and Molecular Biology Course

---

## ข้อมูลเบื้องต้นเกี่ยวกับปฏิบัติการ

**รหัสปฏิบัติการ:** SC153402 
**ระยะเวลา:** 3 ชั่วโมง  
**ลักษณะการทำงาน:** งานเดี่ยว  
**ข้อกำหนดเบื้องต้น:** ความรู้พื้นฐานเกี่ยวกับ central dogma, DNA structure, และ protein synthesis

---

## จุดประสงค์การเรียนรู้ (Learning Objectives)

เมื่อสิ้นสุดปฏิบัติการนี้ นักศึกษาจะสามารถ:

1. สืบค้นข้อมูลจาก NCBI databases (GenBank, Protein Database) ได้อย่างมีประสิทธิภาพและถูกต้อง
2. วิเคราะห์และตีความข้อมูล sequence annotation ที่ปรากฏใน GenBank record ได้อย่างเป็นระบบ
3. ประยุกต์ใช้เครื่องมือพื้นฐานในการวิเคราะห์คุณสมบัติของลำดับ nucleotide และ amino acid เพื่อการออกแบบการทดลองได้

---

## ส่วนที่ 1: เนื้อหาพื้นฐานทางทฤษฎี

### 1.1 Introduction to Bioinformatics

Bioinformatics เป็นสาขาวิชาสหวิทยาการที่บูรณาการความรู้ทางชีววิทยาระดับโมเลกุล วิทยาการคอมพิวเตอร์ สถิติศาสตร์ และคณิตศาสตร์ เข้าด้วยกัน เพื่อวิเคราะห์และตีความข้อมูลชีววิทยาจำนวนมหาศาล (Lesk, 2019) การพัฒนาของเทคโนโลยี DNA sequencing โดยเฉพาะ Next-Generation Sequencing (NGS) ได้ทำให้เกิดการสะสมข้อมูลลำดับพันธุกรรมอย่างรวดเร็ว จำเป็นต้องอาศัยเครื่องมือและวิธีการทาง computational ในการจัดการและวิเคราะห์ข้อมูลเหล่านี้

### 1.2 Biological Sequence Databases: โครงสร้างและความสำคัญ

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

#### 1.2.2 RefSeq Accession Number System

ฐานข้อมูล RefSeq ใช้ระบบหมายเลขอ้างอิง (accession number) ที่มีมาตรฐานเฉพาะ ซึ่งแตกต่างจากฐานข้อมูล GenBank ทั่วไป โดยมีรูปแบบเป็น "two-letter prefix + underscore + six or nine-digit number" เช่น NM_000518.5 หรือ XM_005267557.1 

RefSeq accession numbers แบ่งออกเป็นสองประเภทหลักตามกระบวนการสร้างและระดับการตรวจสอบ:

**Known RefSeq (Curated RefSeq):**
RefSeq records ที่ได้รับการตรวจสอบและคัดกรองโดยผู้เชี่ยวชาญของ NCBI หรือมาจากข้อมูล experimental evidence ที่มีคุณภาพสูง มักมาจาก GenBank cDNA และ EST data

| Prefix | ประเภทโมเลกุล | คำอธิบาย | ตัวอย่าง |
|--------|--------------|----------|----------|
| **NM_** | mRNA (messenger RNA) | Coding transcript ที่ผ่านการตรวจสอบ มี experimental evidence สนับสนุน | NM_000518.5 (Human HBB mRNA) |
| **NR_** | Non-coding RNA | RNA ที่ไม่ถูกแปลเป็นโปรตีน เช่น rRNA, tRNA, lncRNA, miRNA | NR_046018.2 (Human XIST lncRNA) |
| **NP_** | Protein | ลำดับโปรตีนที่สอดคล้องกับ NM_ transcript | NP_000509.1 (Human hemoglobin beta) |
| **NG_** | Genomic region | บริเวณพันธุกรรมที่ไม่ใช่ chromosome ทั้งหมด ใช้เป็น reference สำหรับ gene-specific analysis รวมถึง 5' และ 3' flanking regions (โดยทั่วไป 5,000 bp upstream และ 2,000 bp downstream) | NG_012026.1 (MC1R gene region) |
| **NC_** | Complete chromosome | Chromosome sequence ทั้งหมดจาก reference genome assembly | NC_000023.11 (Human chromosome X) |
| **NT_**, **NW_** | Genomic contig/scaffold | ส่วนประกอบของ genome assembly ที่ยังไม่สมบูรณ์ contig หรือ scaffold | NT_167244.2, NW_009646201.1 |

**Model RefSeq (Predicted RefSeq):**
RefSeq records ที่สร้างขึ้นโดย computational prediction จาก NCBI's eukaryotic genome annotation pipeline หรือ copied จาก computationally annotated submissions ไม่มี direct experimental evidence แต่อิงจาก genome sequence และ algorithms

| Prefix | ประเภทโมเลกุล | คำอธิบาย | ตัวอย่าง |
|--------|--------------|----------|----------|
| **XM_** | mRNA (predicted) | Coding transcript ที่ทำนายจาก genome annotation pipeline | XM_005267557.1 |
| **XR_** | Non-coding RNA (predicted) | Non-coding RNA ที่ทำนายด้วย computational methods | XR_001556.3 |
| **XP_** | Protein (predicted) | โปรตีนที่ทำนายจาก XM_ transcripts | XP_005267614.1 |

**ความสำคัญของการแยกแยะ Known vs. Model RefSeq:**

1. **Known RefSeq (NM_, NR_, NP_)**: มีความน่าเชื่อถือสูงกว่าเนื่องจากได้รับการ validate ด้วย experimental data เหมาะสำหรับการออกแบบ primers, probes, และการศึกษาทางคลินิก

2. **Model RefSeq (XM_, XR_, XP_)**: มีประโยชน์ในการศึกษา alternative splice variants และยีนที่ยังไม่มี experimental evidence เพียงพอ แต่ควรใช้ด้วยความระมัดระวังและควร validate ด้วยการทดลอง

**Version Numbers:**
ทุก RefSeq accession มี version number (เช่น NM_000518.5 โดย ".5" คือ version) version number จะเพิ่มขึ้นเมื่อมีการเปลี่ยนแปลง nucleotide หรือ amino acid sequence การเปลี่ยนแปลง annotation เพียงอย่างเดียวไม่ทำให้ version เปลี่ยน

**Curation Status:**
Known RefSeq records มี curation status ที่ระบุไว้ใน COMMENT block:
- **VALIDATED**: ลำดับผ่านการตรวจสอบโดย NCBI staff
- **REVIEWED**: มีการตรวจสอบทั้งลำดับและข้อมูลเชิงพรรณนา (descriptive information)
- **PROVISIONAL**: ยังไม่ได้รับการตรวจสอบอย่างละเอียด
- **PREDICTED**: สำหรับ Model RefSeq (XM_, XR_, XP_)

**ตัวอย่างการใช้งานจริง:**

สำหรับยีน Human Insulin (INS gene):
- **NC_000011.10**: Human chromosome 11 (complete sequence)
- **NG_007114.1**: Genomic region ของ INS gene (รวม flanking regions สำหรับการศึกษา mutations และ regulatory elements)
- **NM_000207.3**: mRNA transcript ของ insulin (curated, experimentally validated)
- **NP_000198.1**: Insulin protein sequence
- **XM_xxxxxxx**: Alternative transcript variants ที่ทำนายโดย computational methods (ถ้ามี)

**RefSeq Select และ MANE Select:**

NCBI มี initiative พิเศษสำหรับการคัดเลือก "representative transcript" ที่ดีที่สุดสำหรับแต่ละ gene:

- **RefSeq Select**: transcript หนึ่งตัวต่อหนึ่ง gene ที่ได้รับการคัดเลือกโดยพิจารณาจาก expression data, evolutionary conservation, และการใช้งานใน clinical databases (สำหรับ human, mouse, rat)

- **MANE Select** (Matched Annotation from NCBI and EMBL-EBI): collaborative project ระหว่าง NCBI และ EMBL-EBI เพื่อกำหนด standard transcript set สำหรับ clinical reporting ใน human genome โดย MANE Select transcript จะมี 100% identity ระหว่าง RefSeq (NM_) และ Ensembl (ENST) transcripts

#### 1.2.3 GenBank Record Structure

GenBank record ประกอบด้วยส่วนสำคัญดังนี้:

- **LOCUS**: ข้อมูลพื้นฐานเกี่ยวกับลำดับ ได้แก่ ชื่อ ความยาว ประเภทของโมเลกุล และวันที่
- **DEFINITION**: คำอธิบายสั้น ๆ เกี่ยวกับลำดับ
- **ACCESSION**: หมายเลขอ้างอิง (accession number) พร้อม version number ที่ไม่ซ้ำกัน ใช้ในการอ้างอิงและสืบค้น
- **VERSION**: แสดง accession.version (เช่น NM_000518.5)
- **KEYWORDS**: สำหรับ RefSeq จะมีคำว่า "RefSeq" หรือ "RefSeq Select"
- **SOURCE**: ระบุสิ่งมีชีวิตที่มาของลำดับ
- **ORGANISM**: taxonomy classification แบบลำดับชั้น
- **REFERENCE**: บทความวิจัยที่เกี่ยวข้อง
- **COMMENT**: ข้อมูลเพิ่มเติม รวมถึง curation status, genome annotation information
- **FEATURES**: ตารางแสดงลักษณะทางชีววิทยาที่สำคัญ เช่น CDS (coding sequence), mRNA, exon, intron, regulatory elements
- **ORIGIN**: ลำดับนิวคลีโอไทด์จริง

### 1.3 Fundamental Concepts in Sequence Analysis

#### 1.3.1 FASTA Format

FASTA format เป็นรูปแบบมาตรฐานในการจัดเก็บและแลกเปลี่ยนข้อมูลลำดับชีววิทยา ประกอบด้วย:
- **Header line**: เริ่มต้นด้วยเครื่องหมาย `>` ตามด้วยชื่อหรือรหัสของลำดับ
- **Sequence lines**: ลำดับนิวคลีโอไทด์หรือกรดอะมิโน โดยทั่วไปจัดเรียงเป็นบรรทัดละ 60-80 ตัวอักษร

ตัวอย่าง: nucleotide fasta
```
>NM_000518.5 Homo sapiens hemoglobin subunit beta (HBB), mRNA
ACATTTGCTTCTGACACAACTGTGTTCACTAGCAACCTCAAACAGACACCATGGTGCATCTGACTCCTG
AGGAGAAGTCTGCCGTTACTGCCCTGTGGGGCAAGGTGAACGTGGATGAAGTTGGTGGTGAGGCCCTGG
```
ตัวอย่าง: amino acid fasta
```
>NP_000509.1 hemoglobin subunit beta [Homo sapiens]
MVHLTPEEKSAVTALWGKVNVDEVGGEALGRLLVVYPWTQRFFESFGDLSTPDAVMGNPKVKAHGKKVLG
AFSDGLAHLDNLKGTFATLSELHCDKLHVDPENFRLLGNVLVCVLAHHFGKEFTPPVQAAYQKVVAGVAN
ALAHKYH
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
- ประมาณขนาดของโปรตีน: ใช้เทียบตำแหน่งของแถบโปรตีนในการทำ SDS-PAGE หรือ Western Blot ว่าโปรตีนที่เราสนใจควรจะปรากฏที่ขนาดเท่าไหร่
- การกรองโมเลกุล: ใช้เลือกขนาดของไส้กรอง (Cut-off filter) หรือชนิดของเรซินในการทำ Gel Filtration Chromatography

**Theoretical Isoelectric Point (pI)**: ค่า pH ที่โปรตีนมี net charge เป็นศูนย์ ขึ้นอยู่กับองค์ประกอบของกรดอะมิโนที่มีกลุ่ม ionizable คุณสมบัตินี้มีความสำคัญต่อ:
- Isoelectric focusing (IEF): ใช้ในเทคนิคแยกโปรตีนตามค่า pI บนเจลที่มี pH gradient
- Ion exchange chromatography: ใช้เลือกชนิดของ Buffer และ Resin ถ้า pH ของสารละลายต่ำกว่า pI โปรตีนจะมีประจุบวก (จับกับ Cation exchange resin) แต่ถ้า pH สูงกว่า pI โปรตีนจะมีประจุลบ (จับกับ Anion exchange resin)
- Protein solubility และ crystallization: โดยทั่วไปโปรตีนจะละลายน้ำได้น้อยที่สุดเมื่ออยู่ในสภาพ pH เท่ากับค่า pI ของมัน (เพราะไม่มีประจุผลักกัน ทำให้โปรตีนจับตัวกันตกตะกอน) นักวิจัยจึงมักเลี่ยงค่า pH นี้หากต้องการให้โปรตีนละลาย หรือจงใจใช้ pH นี้หากต้องการตกตะกอนโปรตีน

**GRAVY Score** (Grand Average of Hydropathicity): เป็นค่าดัชนีที่บอกว่าโปรตีนตัวนั้น "เกลียดน้ำ" (Hydrophobic) หรือ "ชอบน้ำ" (Hydrophilic) โดยรวมมากแค่ไหน คำนวณจากการเฉลี่ยค่า Hydropathy (ตามเกณฑ์ของ Kyte & Doolittle, 1982) ของกรดอะมิโนทุกตัวในสาย

**Instability Index**: เป็นการคำนวณทางสถิติเพื่อทำนายว่าโปรตีนนี้จะมีความ "เสถียร" (Stable) หรือ "สลายตัวง่าย" (Unstable) เมื่ออยู่ในหลอดทดลอง (in vitro)

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

5. หากต้องการคำนวณความเข้มข้นของ purified protein โดยการวัด absorbance ที่ 280 nm และได้ค่า A₂₈₀ = 0.5 (ใช้ cuvette 1 cm path length) ความเข้มข้นของโปรตีนเป็นเท่าใด (หน่วย mg/mL)?
   
   *สูตร:* 
   $$C (\text{mg/mL}) = \frac{A_{280} \times \text{MW (Da)}}{\varepsilon \text{ (M}^{-1}\text{cm}^{-1}\text{)}}$$
   
   (หมายเหตุ: 1 M = 1 mol/L; ต้องแปลงหน่วยอย่างเหมาะสม)

6. วิเคราะห์ hydropathy plot (Kyte & Doolittle scale):
   - มี hydrophobic stretches ที่ยาวพอที่จะเป็น transmembrane domain (~ 20-25 residues) หรือไม่?

---

## ส่วนที่ 4: แหล่งข้อมูลเพิ่มเติมและการอ่านเพิ่มเติม

### 4.1 Web Resources และ Tutorials

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

### 4.2 คำศัพท์สำคัญและคำจำกัดความ

| คำศัพท์ | คำจำกัดความ |
|---------|-------------|
| **Accession Number** | รหัสอ้างอิงเฉพาะที่ใช้ระบุ sequence record ในฐานข้อมูล ไม่เปลี่ยนแปลงแม้ sequence จะถูกแก้ไข โดย RefSeq ใช้รูปแบบ two-letter prefix + underscore + six-digit number พร้อม version number (เช่น NM_000518.5) |
| **Annotation** | การเพิ่มข้อมูลเชิงชีววิทยาลงใน sequence record เช่น ตำแหน่งของ genes, regulatory elements, protein domains |
| **CDS (Coding Sequence)** | ส่วนของ nucleotide sequence ที่แปลเป็น amino acids (ไม่รวม introns ใน genomic DNA) เริ่มจาก start codon (ATG) ถึง stop codon |
| **Curated RefSeq** | RefSeq records ที่ได้รับการตรวจสอบและ validate โดยผู้เชี่ยวชาญ (Known RefSeq: NM_, NR_, NP_, NG_, NC_) มีความน่าเชื่อถือสูงกว่า Model RefSeq |
| **E-value (Expect value)** | ค่าทางสถิติที่บ่งบอกความน่าจะเป็นที่ sequence alignment จะเกิดขึ้นโดยบังเอิญ ยิ่งค่าต่ำยิ่งมีนัยสำคัญ (E-value < 0.01 ถือว่ามี significance สูง) |
| **FASTA format** | รูปแบบมาตรฐานสำหรับจัดเก็บ biological sequences ประกอบด้วย header line (>) และ sequence lines |
| **GenBank** | ฐานข้อมูล nucleotide sequences ของ NCBI ที่เก็บข้อมูล DNA และ RNA sequences จากทุกสิ่งมีชีวิต เป็น archival database ที่มีความซ้ำซ้อนสูง |
| **Homology** | ความสัมพันธ์ระหว่าง sequences ที่มาจาก common ancestor เดียวกัน แบ่งเป็น orthology (เกิดจาก speciation) และ paralogy (เกิดจาก gene duplication) |
| **Known RefSeq** | RefSeq records ที่มา mainly จาก experimental data (GenBank cDNA/EST) ใช้ prefixes: NM_, NR_, NP_, NG_, NC_ แตกต่างจาก Model RefSeq ที่เป็น computational predictions |
| **MANE Select** | Matched Annotation from NCBI and EMBL-EBI - transcript ที่ได้รับการคัดเลือกเป็น clinical standard มี 100% identity ระหว่าง RefSeq และ Ensembl annotations |
| **Model RefSeq** | RefSeq records ที่สร้างจาก computational prediction (prefixes: XM_, XR_, XP_) ไม่มี direct experimental evidence แต่มีประโยชน์ในการศึกษา alternative transcripts |
| **ORF (Open Reading Frame)** | ลำดับระหว่าง start codon และ stop codon ที่สามารถแปลเป็น protein ได้ DNA แต่ละ strand มี 3 possible reading frames (รวม 6 frames ทั้ง 2 strands) |
| **RefSeq** | Reference Sequence database - non-redundant, curated collection ของ genomic, transcript, และ protein sequences ที่มีคุณภาพสูงกว่า GenBank |
| **RefSeq Select** | Representative transcript หนึ่งตัวต่อหนึ่ง gene ที่ได้รับการคัดเลือกตาม expression, conservation, และ clinical usage (สำหรับ human, mouse, rat) |
| **UTR (Untranslated Region)** | บริเวณใน mRNA ที่ไม่ถูกแปลเป็นโปรตีน แบ่งเป็น 5' UTR (upstream ของ start codon) และ 3' UTR (downstream ของ stop codon) มีบทบาทในการควบคุม translation และ mRNA stability |
| **Version Number** | เลขหลังจุดใน accession number (เช่น .5 ใน NM_000518.5) เพิ่มขึ้นทุกครั้งที่มีการเปลี่ยนแปลง sequence แต่ไม่เปลี่ยนเมื่อแก้ annotation เพียงอย่างเดียว |

---

**เอกสารประกอบการสอนฉบับนี้จัดทำโดย:** อ.ทศพล เตโช 
**สถาบัน:** สาขาวิชาชีววิทยา คณะวิทยาศาสตร์ มหาวิทยาลัยขอนแก่น
**วันที่จัดทำ:** 2/12/2025
**เวอร์ชัน:** 1.0  
