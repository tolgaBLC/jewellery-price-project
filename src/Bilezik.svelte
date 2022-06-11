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
  let alisKariBlz = 0;
  let satisKariBlz = 0;
  let satisMilyemBlz = 0.932;
  let alisMilyemBlz = 0.912;
  let alisYuvarlamaBlz = 0;
  let satisYuvarlamaBlz = 0;

  const toggle = () => (open = !open);
  function increaseSatisMilyem() {
    satisMilyemBlz = Math.round((satisMilyemBlz + 0.001) * 1000) / 1000;
  }
  function decreaseSatisMilyem() {
    satisMilyemBlz = Math.round((satisMilyemBlz - 0.001) * 1000) / 1000;
  }
  function increaseAlisMilyem() {
    alisMilyemBlz = Math.round((alisMilyemBlz + 0.001) * 1000) / 1000;
  }
  function decreaseAlisMilyem() {
    alisMilyemBlz = Math.round((alisMilyemBlz - 0.001) * 1000) / 1000;
  }
  function increaseAlisKari() {
    alisKariBlz += 1;
  }
  function decreaseAlisKari() {
    alisKariBlz -= 1;
  }
  function increaseSatisKari() {
    satisKariBlz += 1;
  }
  function decreaseSatisKari() {
    satisKariBlz -= 1;
  }
  function increaseAlisYuvarlama() {
    alisYuvarlamaBlz += 5;
    alisKariBlz += 1;
    alisKariBlz -= 1;
  }
  function decreaseAlisYuvarlama() {
    alisYuvarlamaBlz -= 5;
    alisKariBlz += 1;
    alisKariBlz -= 1;
  }
  function increaseSatisYuvarlama() {
    satisYuvarlamaBlz += 5;
    satisKariBlz += 1;
    satisKariBlz -= 1;
  }
  function decreaseSatisYuvarlama() {
    satisYuvarlamaBlz -= 5;
    satisKariBlz += 1;
    satisKariBlz -= 1;
  }
  function adjustBilezikAlis(num) {
    if (alisYuvarlamaBlz !== 0) {
      return roundDown(num, alisYuvarlamaBlz);
    } else {
      return parseInt(num);
    }
  }
  function adjustBilezikSatis(num) {
    if (satisYuvarlamaBlz !== 0) {
      return roundUp(num, satisYuvarlamaBlz);
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
          >Bilezik 22k: <Badge>Alış:</Badge>
          {adjustBilezikAlis($alis * alisMilyemBlz - alisKariBlz)}
          <Badge>Satış:</Badge>
          {adjustBilezikSatis($satis * satisMilyemBlz + satisKariBlz)}</span
        >
      </Card></Col
    >
    <div>
      <Button color="danger" on:click="{toggle}">Bilezik Ayarları</Button>
      <Modal isOpen="{open}" toggle="{toggle}">
        <ModalHeader toggle="{toggle}">Bilezik Ayarları</ModalHeader>
        <ModalBody>
          <Col sm="auto"
            ><Card body class="mb-3"
              ><span
                ><Button color="danger" on:click="{decreaseSatisMilyem}"
                  >-</Button
                > Toptancıdan Gelişi:
                {satisMilyemBlz}
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
                {alisMilyemBlz}
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
                {alisKariBlz} TL
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
                {satisKariBlz} TL
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
                {alisYuvarlamaBlz} TL
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
                {satisYuvarlamaBlz} TL
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
