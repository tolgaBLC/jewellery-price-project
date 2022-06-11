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
  let alisKariResat = 0;
  let satisKariResat = 0;
  let satisMilyemResat = 6.65;
  let alisMilyemResat = 6.6;
  let alisYuvarlamaResat = 0;
  let satisYuvarlamaResat = 0;

  const toggle = () => (open = !open);
  function increaseSatisMilyem() {
    satisMilyemResat = Math.round((satisMilyemResat + 0.005) * 1000) / 1000;
  }
  function decreaseSatisMilyem() {
    satisMilyemResat = Math.round((satisMilyemResat - 0.005) * 1000) / 1000;
  }
  function increaseAlisMilyem() {
    alisMilyemResat = Math.round((alisMilyemResat + 0.005) * 1000) / 1000;
  }
  function decreaseAlisMilyem() {
    alisMilyemResat = Math.round((alisMilyemResat - 0.005) * 1000) / 1000;
  }
  function increaseAlisKari() {
    alisKariResat += 1;
  }
  function decreaseAlisKari() {
    alisKariResat -= 1;
  }
  function increaseSatisKari() {
    satisKariResat += 1;
  }
  function decreaseSatisKari() {
    satisKariResat -= 1;
  }
  function increaseAlisYuvarlama() {
    alisYuvarlamaResat += 5;
    alisKariResat += 1;
    alisKariResat -= 1;
  }
  function decreaseAlisYuvarlama() {
    alisYuvarlamaResat -= 5;
    alisKariResat += 1;
    alisKariResat -= 1;
  }
  function increaseSatisYuvarlama() {
    satisYuvarlamaResat += 5;
    satisKariResat += 1;
    satisKariResat -= 1;
  }
  function decreaseSatisYuvarlama() {
    satisYuvarlamaResat -= 5;
    satisKariResat += 1;
    satisKariResat -= 1;
  }
  function adjustResatAlis(num) {
    if (alisYuvarlamaResat !== 0) {
      return roundDown(num, alisYuvarlamaResat);
    } else {
      return parseInt(num);
    }
  }
  function adjustResatSatis(num) {
    if (satisYuvarlamaResat !== 0) {
      return roundUp(num, satisYuvarlamaResat);
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
          >Reşat Lira: <Badge>Alış:</Badge>
          {adjustResatAlis($alis * alisMilyemResat - alisKariResat)}
          <Badge>Satış:</Badge>
          {adjustResatSatis($satis * satisMilyemResat + satisKariResat)}</span
        >
      </Card></Col
    >
    <div>
      <Button color="danger" on:click="{toggle}">Reşat Lira Ayarları</Button>
      <Modal isOpen="{open}" toggle="{toggle}">
        <ModalHeader toggle="{toggle}">Reşat Lira Ayarları</ModalHeader>
        <ModalBody>
          <Col sm="auto"
            ><Card body class="mb-3"
              ><span
                ><Button color="danger" on:click="{decreaseSatisMilyem}"
                  >-</Button
                > Toptancıdan Gelişi:
                {satisMilyemResat}
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
                {alisMilyemResat}
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
                {alisKariResat} TL
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
                {satisKariResat} TL
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
                {alisYuvarlamaResat} TL
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
                {satisYuvarlamaResat} TL
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
