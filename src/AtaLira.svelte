<script>
  import {
    Styles,
    Badge,
    Col,
    Row,
    Card,
    Button,
    Modal,
    ModalBody,
    ModalFooter,
    ModalHeader,
  } from "sveltestrap";
  import { alis } from "./stores.js";
  import { satis } from "./stores.js";
  let open = false;
  let alisKariAta = 0;
  let satisKariAta = 0;
  let satisMilyemAta = 6.65;
  let alisMilyemAta = 6.6;
  let alisYuvarlamaAta = 0;
  let satisYuvarlamaAta = 0;

  const toggle = () => (open = !open);
  function increaseSatisMilyem() {
    satisMilyemAta = Math.round((satisMilyemAta + 0.005) * 1000) / 1000;
  }
  function decreaseSatisMilyem() {
    satisMilyemAta = Math.round((satisMilyemAta - 0.005) * 1000) / 1000;
  }
  function increaseAlisMilyem() {
    alisMilyemAta = Math.round((alisMilyemAta + 0.005) * 1000) / 1000;
  }
  function decreaseAlisMilyem() {
    alisMilyemAta = Math.round((alisMilyemAta - 0.005) * 1000) / 1000;
  }
  function increaseAlisKari() {
    alisKariAta += 1;
  }
  function decreaseAlisKari() {
    alisKariAta -= 1;
  }
  function increaseSatisKari() {
    satisKariAta += 1;
  }
  function decreaseSatisKari() {
    satisKariAta -= 1;
  }
  function increaseAlisYuvarlama() {
    alisYuvarlamaAta += 5;
    alisKariAta += 1;
    alisKariAta -= 1;
  }
  function decreaseAlisYuvarlama() {
    alisYuvarlamaAta -= 5;
    alisKariAta += 1;
    alisKariAta -= 1;
  }
  function increaseSatisYuvarlama() {
    satisYuvarlamaAta += 5;
    satisKariAta += 1;
    satisKariAta -= 1;
  }
  function decreaseSatisYuvarlama() {
    satisYuvarlamaAta -= 5;
    satisKariAta += 1;
    satisKariAta -= 1;
  }
  function adjustAtaAlis(num) {
    if (alisYuvarlamaAta !== 0) {
      return roundDown(num, alisYuvarlamaAta);
    } else {
      return parseInt(num);
    }
  }
  function adjustAtaSatis(num) {
    if (satisYuvarlamaAta !== 0) {
      return roundUp(num, satisYuvarlamaAta);
    } else {
      return parseInt(num);
    }
  }
  function roundDown(num, rNum) {
    return Math.floor(num / rNum) * rNum;
  }
  function roundUp(num, rNum) {
    return Math.ceil(num / rNum) * rNum;
  }
</script>

<Styles />
<Card body color="dark">
  <Row>
    <Col sm="5"
      ><Card body color="warning" class="mb-3"
        ><span
          >Ata Lira: <Badge>Alış:</Badge>
          {adjustAtaAlis($alis * alisMilyemAta - alisKariAta)}
          <Badge>Satış:</Badge>
          {adjustAtaSatis($satis * satisMilyemAta + satisKariAta)}</span
        >
      </Card></Col
    >
    <div>
      <Button color="danger" on:click="{toggle}">Ata Lira Ayarları</Button>
      <Modal isOpen="{open}" toggle="{toggle}">
        <ModalHeader toggle="{toggle}">Ata Lira Ayarları</ModalHeader>
        <ModalBody>
          <Col sm="auto"
            ><Card body class="mb-3"
              ><span
                ><Button color="danger" on:click="{decreaseSatisMilyem}"
                  >-</Button
                > Toptancıdan Gelişi:
                {satisMilyemAta}
                <Button color="success " on:click="{increaseSatisMilyem}"
                  >+</Button
                ></span
              ></Card
            ></Col
          >
          <Col sm="auto"
            ><Card body class="mb-3"
              ><span
                ><Button color="danger" on:click="{decreaseAlisMilyem}"
                  >-</Button
                > Toptancının Alışı:
                {alisMilyemAta}
                <Button color="success " on:click="{increaseAlisMilyem}"
                  >+</Button
                ></span
              ></Card
            ></Col
          >
          <Col sm="auto"
            ><Card body class="mb-3"
              ><span
                ><Button color="danger" on:click="{decreaseAlisKari}">-</Button>

                Alış Karı:
                {alisKariAta} TL
                <Button color="success " on:click="{increaseAlisKari}">+</Button
                ></span
              ></Card
            ></Col
          >
          <Col sm="auto"
            ><Card body class="mb-3"
              ><span
                ><Button color="danger" on:click="{decreaseSatisKari}">-</Button
                >

                Satış Karı:
                {satisKariAta} TL
                <Button color="success " on:click="{increaseSatisKari}"
                  >+</Button
                ></span
              ></Card
            ></Col
          >
          <Col sm="auto"
            ><Card body class="mb-3"
              ><span
                ><Button color="danger" on:click="{decreaseAlisYuvarlama}"
                  >-</Button
                >

                Alış Yuvarlama:
                {alisYuvarlamaAta} TL
                <Button color="success " on:click="{increaseAlisYuvarlama}"
                  >+</Button
                ></span
              ></Card
            ></Col
          >
          <Col sm="auto"
            ><Card body class="mb-3"
              ><span
                ><Button color="danger" on:click="{decreaseSatisYuvarlama}"
                  >-</Button
                >

                Satış Yuvarlama:
                {satisYuvarlamaAta} TL
                <Button color="success " on:click="{increaseSatisYuvarlama}"
                  >+</Button
                ></span
              ></Card
            ></Col
          >
        </ModalBody>
        <ModalFooter>
          <!-- <Button color="primary" on:click="{toggle}">Kaydet</Button> -->
          <Button color="secondary" on:click="{toggle}">Kapat</Button>
        </ModalFooter>
      </Modal>
    </div>
  </Row>
</Card>

<style>
  span {
    font-weight: bold;
    display: inline-block;
    /* font-size: 1.4em;
      background: linear-gradient(to right, black 90%, white 100%);
      -webkit-background-clip: text;
      -webkit-text-fill-color: transparent; */
  }
</style>
